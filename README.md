# nix-configs
Nix configuration for workstation setup. Heavy usage of [nix-darwin](https://github.com/LnL7/nix-darwin)

## Bootstrapping:

```sh
# I found some good resources but they seem to do a bit too much (maybe from a time when there were more bugs).
# So here's a minimal Gist which worked for me as an install on a new M1 Pro.
# Inspired by https://github.com/malob/nixpkgs I highly recommend looking at malob's repo for a more thorough configuration
#
# Let's get started
#
# Let's install nix (at the time of writing this is version 2.5.1
curl -L https://nixos.org/nix/install | sh

# I might not have needed to, but I rebooted
mkdir -p ~/.config/nix

# Emable nix-command and flakes to bootstrap 
cat <<EOF > ~/.config/nix/nix.conf
command flakes
EOF

# Get this repo
cd ~/.config
git clone git@github.com:mkantzer/nix-configs.git

# Until this is addressed https://github.com/LnL7/nix-darwin/issues/149
sudo mv /etc/nix/nix.conf /etc/nix/.nix-darwin.bkp.nix.conf
# Build the configuration
nix build .#darwinConfigurations.mikes-mbp-3.system
./result/sw/bin/darwin-rebuild switch --flake .
# Enjoy!
```


## Sources:

- [Primary inspiration gist](https://gist.github.com/jmatsushita/5c50ef14b4b96cb24ae5268dab613050)
- [Inspiration's Inspiration](https://github.com/malob/nixpkgs)
- [Additional Inspiration](https://github.com/MatthiasBenaets/nixos-config/blob/master/darwin.org)
- Some ideas: https://github.com/mitchellh/nixos-config 