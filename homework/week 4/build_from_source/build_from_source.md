A recent obsession of mine has been this file explorer called [Yazi](https://yazi-rs.github.io/docs/installation) that is written in Rust - super fast, and well-designed for *nix*-type systems. I think it would be fun to build it from source as it has some dependencies you need to tweak in order to get it running nicely.

## Installing make and gcc

These are part of the GNU toolchain and are used for building and compiling programs and are standard for many Linux projects. Make specifically automates the build process by using a makefile that lists non-source programs and libraries and instructions on how to create them.

`apt install make gcc` 

## Prerequisites and Extensions
These are needed to make sure everything fits together nicely (PDF/Video previous, archive previews and such)

`apt install file`

These are the other "extensions" that make Yazi look, and feel much nicer:
`ffmpegthumbnailer 7z jq poppler fd rg fzf zocide ImageMagick xclip`

I had to manually figure out the package names and installation instructions for most of those as they vary.

`apt install ffmpegthumbnailer p7zip-full jq poppler-utils fd-find ripgrep fzf imagemagick xclip`

Bash command for installing zoxide, and nerd-fonts respectively
`curl -sS https://raw.githubusercontent.com/ajeetdsouza/zoxide/main/install.sh | bash`\

`bash -c "$(curl -fsSL https://raw.githubusercontent.com/officialrajdeepsingh/nerd-fonts-installer/main/install.sh)"` - I installed Noto8

Looks like all these installations went through without issues

### Installing Rust toolchain
`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`

### Configuring environment variables for Rust

Added `$HOME/.cargo/bin)`  to .zshenv since I use zsh
`source ~/.zshenv` Activating the newly updated environment file

`rustup update`

### Cloning and building 
```
git clone https://github.com/sxyazi/yazi.git
cd yazi
cargo build --release --locked
```

### Running

`~/yazi/target/release$ ./yazi`
You can add this to your environment variable to call yazi from anywhere
