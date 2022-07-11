# How to create ExoTool docker image
- ## W.I.P
- ### how should we build it?  
	- get the dockerfile for the rust container  
	- add a layer to the [docker file](https://linuxhandbook.com/modifying-docker-image/)  
	-  
	  ```
	  	  FROM Rust:buster // use specific version not a tag for stability ? might not matter
	  	  
	  	  ENV ... // enviroment variables 
	  	  
	  	  RUN apk add... <dependencies>; \
	  	  	cargo build --release substrate node;
	  	  	// we could use curl with a hosted text file that has all the commands
	  	      // that might not be as secure but more convinient
	  	      // could compile it on run, but would be smarter and faster to distribute bin
	  	      // distributing a bin would be best along side a checksum in the image
	  	      // we need to host the binary somewhere and distribute the dockerfile with a checksum
	  	  	// need to have an install script that moves the bin to the right path, etc
	  	      
	  	  VOLUME ...
	  	      
	  	  ENTRYPOINT ["<NodeName>", "<Default Param1>", "<Default Param2>"]
	  ```
	- Rust destributes the checksum inside the [dockerfile](https://github.com/rust-lang/docker-rust/blob/cdceae24a8dfcad5d5c85cf4a949c340437a0d01/1.62.0/buster/Dockerfile) with a run command  
		-  
		  ```
		  		  FROM buildpack-deps:buster
		  		  
		  		  ENV RUSTUP_HOME=/usr/local/rustup \
		  		      CARGO_HOME=/usr/local/cargo \
		  		      PATH=/usr/local/cargo/bin:$PATH \
		  		      RUST_VERSION=1.62.0
		  		  
		  		  RUN set -eux; \
		  		      dpkgArch="$(dpkg --print-architecture)"; \
		  		      case "${dpkgArch##*-}" in \
		  		          amd64) rustArch='x86_64-unknown-linux-gnu'; rustupSha256='3dc5ef50861ee18657f9db2eeb7392f9c2a6c95c90ab41e45ab4ca71476b4338' ;; \
		  		          armhf) rustArch='armv7-unknown-linux-gnueabihf'; rustupSha256='67777ac3bc17277102f2ed73fd5f14c51f4ca5963adadf7f174adf4ebc38747b' ;; \
		  		          arm64) rustArch='aarch64-unknown-linux-gnu'; rustupSha256='32a1532f7cef072a667bac53f1a5542c99666c4071af0c9549795bbdb2069ec1' ;; \
		  		          i386) rustArch='i686-unknown-linux-gnu'; rustupSha256='e50d1deb99048bc5782a0200aa33e4eea70747d49dffdc9d06812fd22a372515' ;; \
		  		          *) echo >&2 "unsupported architecture: ${dpkgArch}"; exit 1 ;; \
		  		      esac; \
		  		      url="https://static.rust-lang.org/rustup/archive/1.24.3/${rustArch}/rustup-init"; \
		  		      wget "$url"; \
		  		      echo "${rustupSha256} *rustup-init" | sha256sum -c -; \
		  		      chmod +x rustup-init; \
		  		      ./rustup-init -y --no-modify-path --profile minimal --default-toolchain $RUST_VERSION --default-host ${rustArch}; \
		  		      rm rustup-init; \
		  		      chmod -R a+w $RUSTUP_HOME $CARGO_HOME; \
		  		      rustup --version; \
		  		      cargo --version; \
		  		      rustc --version;
		  ```
	- **the rust Dockerfile uses rustup.**  
	- What we should do is distribute bins like rust does:  
		-  
		  ```
		  		  	url="https://static.rust-lang.org/rustup/archive/1.24.3/${rustArch}/rustup-init"; \
		  		      wget "$url";
		  ```
		- we need to host a bin and dockerfile.  
	- We need to find a safe way to distribute the files and checksum. man in the middle attacks?  
	- An [`ENTRYPOINT`](https://docs.docker.com/engine/reference/builder/#entrypoint) allows you to configure a container that will run as an executable  
		- The Entry point should auto exec some paramiters like ports? or should that be up to the users docker run command?  
	- The [`VOLUME`](https://docs.docker.com/engine/reference/builder/#volume) instruction creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers.