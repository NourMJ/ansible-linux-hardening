# Ansible Role: Linux Server Hardening

This is a simple Ansible role that automates the basic security hardening of a new Red Hat-based Linux server (RHEL, CentOS, Fedora, etc.). It's designed to be run on a fresh server to establish a secure baseline.

---

## 🚀 Features

This role performs the following actions:

* **SSH Security:**
    * Disables root login over SSH (`PermitRootLogin no`) in `/etc/ssh/sshd_config`.
* **User Management:**
    * Creates a new administrative user named `admin_user`.
    * Grants that user password-less `sudo` privileges by adding them to the `wheel` group.
* **Firewall Configuration:**
    * Installs the `firewalld` package.
    * Starts and enables the `firewalld` service.
    * Configures the firewall to **block all incoming traffic** *except* for `ssh`.

---

## ⚠️ Security Warning: Hardcoded Password

**This project is a portfolio example.** In its current state, the password for `admin_user` is **hardcoded** inside the `roles/server_hardening/tasks/main.yml` file.

**Do not use this in a real production environment as-is.** The correct way to handle this is to use Ansible Vault for the password or pass it as a variable at runtime.

---

## 📦 Requirements

* Ansible (on the control node).
* A target host running a Red Hat-based distribution (RHEL, CentOS, Fedora).
* Python 3 on the target host (usually present by default).

---

## ⚙️ How to Use

This project is set up to run on `localhost` by default.

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/NourMJ/ansible-linux-hardening.git](https://github.com/NourMJ/ansible-linux-hardening.git)
    cd ansible-linux-hardening
    ```

2.  **Update the Inventory (Optional):**
    * The `inventory` file is pre-configured to run on `localhost`.
    * To run this on a *remote* server, edit the `inventory` file and change `localhost` to your server's IP address or hostname:
        ```ini
        [my_server]
        192.168.1.100
        ```
    * If you change the inventory, you will need to provide connection flags to the `ansible-playbook` command (like `-u root --ask-pass`).

3.  **Run the Playbook:**
    ```bash
    ansible-playbook -i inventory playbook.yml
    ```
    This will apply all the hardening tasks defined in the role. You can run it multiple times; it is idempotent.

---

## License

[MIT](https://choosealicense.com/licenses/mit/)
