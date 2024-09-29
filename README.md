# Fixing `WSL2` Networking Issue: Ubuntu Can Ping but `apt-get update` Fails

## Problem:
In `WSL2`, Ubuntu is able to ping external websites (e.g., Google) but cannot reach package repositories when running `apt-get update`. This is typically due to networking configuration issues with `Hyper-V` and DNS settings.

## Solution:

Follow these steps to resolve the issue:

1. `Open Hyper-V Manager` as an administrator.
2. Select your PC and go to `Virtual Switch Manager`.
3. Choose the `WSL (Hyper-V firewall)` switch.
4. Set the switch to `External Network` and select the network card through which your traffic flows.
5. Apply the changes.

6. In the WSL2 Terminal, configure the IP address:
    - Run the following commands:
    ```bash
    sudo ip addr flush dev eth0
    sudo dhclient eth0
    ```

7. Once completed, try running `sudo apt-get update` again. The package manager should now be able to access the repositories.

## Note:
This solution worked for me while using `Ubuntu 24.02.6`.

## Credit:
This solution was originally identified on `StackOverflow` and later shared by **Abdullah-bin-hasan** on the `WSL GitHub issue` page.

Source: [StackOverflow solution](https://stackoverflow.com/a/62438375/10853017) | [GitHub issue shared by Abdullah-bin-hasan](https://github.com/microsoft/WSL/issues/5971)
