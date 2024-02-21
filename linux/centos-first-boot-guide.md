### Viewing Network Interfaces with `ip addr`

1. **Open a Terminal**: Access your terminal.

2. **List Network Interfaces**: To see all your network interfaces along with their current status, use the following command:
   ```sh
   ip addr
   ```
   This command displays a list of all network interfaces, their IP addresses if assigned, and other details. Note the name of the interface you wish to manage (e.g., `enp0s3`).

### Editing Network Interface Configuration to Auto-start on Boot

1. **Navigate to Network Scripts Directory**: Configuration files for network interfaces are located in `/etc/sysconfig/network-scripts/`. The file you're interested in will follow the naming convention `ifcfg-<interface name>`.

2. **Edit the Configuration File**: Use a text editor like `nano` or `vi` to edit the interface's configuration file. For example, if your interface is named `enp0s3`, you would edit its configuration with:
   ```sh
   sudo nano /etc/sysconfig/network-scripts/ifcfg-enp0s3
   ```
   Replace `nano` with `vi` or your preferred editor as needed.

3. **Set ONBOOT Option to Yes**: Find or add a line starting with `ONBOOT=` and set it to `yes`:
   ```plaintext
   ONBOOT=yes
   ```
   This ensures the interface will automatically activate on boot.

4. **Save and Exit the Editor**: After modifying the configuration, save your changes and exit the editor.

### Managing Network Interface State with `ifup` and `ifdown`

- **Bringing an Interface Up**: To activate an interface immediately without rebooting, use the `ifup` command followed by the interface name. For example:
  ```sh
  sudo ifup enp0s3
  ```
  This command activates the `enp0s3` interface.

- **Bringing an Interface Down**: Conversely, to deactivate an interface, use the `ifdown` command followed by the interface name. For example:
  ```sh
  sudo ifdown enp0s3
  ```
  This command deactivates the `enp0s3` interface.

### Verifying the Changes

- **Verify Interface Status with `ip addr`**: After using `ifup` or `ifdown`, you can verify the status of your interface by running `ip addr` again. Look for your interface name to see if it's listed as `<UP>` or `<DOWN>`.

- **Ensure Automatic Activation on Boot**: To verify that your interface is set to activate on boot, you can either reboot to check its status or inspect the `ifcfg-<interface name>` file to ensure the `ONBOOT=yes` setting is present.

By following these steps, you will be able to manage your network interfaces in CentOS, ensuring they are configured to automatically activate on boot and manually controlling their state as needed.
