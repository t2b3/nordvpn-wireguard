# nordvpn-wireguard
Aim of this Bash shell script operating under Linux:
Route all network traffic through a Wireguard tunnel by using network namespaces

The shell script provided is adapted to the use with NordVPN and provides an alternative to the policy-based routing that NordVPN applies by default in Linux environments.
Please adapt the script to your liking and to your environment (like network interfaces, wpa_supplicant configuration files and DNS resolvers).

You may place the shell script into `$PATH` and mark as executable if necessary.

## Enable isolation of the real network interfaces
Run `wgphys up` to isolate/assign the real network interfaces into the namespace `physical`
and to route all the traffic from/to the root namespace over the Wireguard interface `wgvpn0` that is left in the root namespace. The real network devices are no longer accessible in the root namespace thus preventing any leak.

Alternatively, you may run `wgphys up <conf-identifier>` to do the same but configure the Wireguard interface with a particular configuration file.

## Disable isolation of the real network interfaces
Run `wgphys down` to rollback the isolation created by `wgphys up`.
This will disable the complete network stack so you need to bring it up by your own.

## Breakout
Run `wgphys exec <command> <command_arguments>` to run the `<command>` in the namespace `physical` instead of the root namespace (thus "breaking out"). In this instance, the run command can then access the real network interfaces that reside within the namespace `physical` and uses the DNS name resolution configured for that namespace.

Please also consider the comments within the shell script and consult the sources stated within in case of further questions.
