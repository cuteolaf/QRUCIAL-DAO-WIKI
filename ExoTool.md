- # Exotool docker deployment  
	- ## Dockerfile creation / structure  
		- Rough idea: [Docs](https://docs.docker.com/engine/reference/builder/)  
		  ```
		  FROM rust:buster // this is the base / parent image we modify, doesent have to be debian options: slim-buster, bullseye, alpine
		  		  
		  ENV ... // any env. variables we need to set
		  		  
		  RUN 	// This is the install script that should grab and deploy the binary
		  		  		// We need to checksum the binaries here too
		  		          
		  VOLUME ...	// mount point / the files shared between the docker and the system
		  		  
		  ENTRYPOINT ["<Command>", "<Param1>"] // the command to auto-exec when run
		  ```
		- Properly made docker file (for reference) ([rust](https://github.com/rust-lang/docker-rust/blob/cdceae24a8dfcad5d5c85cf4a949c340437a0d01/1.62.0/buster/Dockerfile)):  
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
    	- An [`ENTRYPOINT`](https://docs.docker.com/engine/reference/builder/#entrypoint) allows you to configure a container that will run as an executable  
    		- The Entry point should auto exec some paramiters like ports? or should that be up to the users docker run command?  
    	- The [`VOLUME`](https://docs.docker.com/engine/reference/builder/#volume) instruction creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers.  