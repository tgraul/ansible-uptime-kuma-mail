Uptime Kuma Monitoring with Nginx, Postfix, and OpenDKIM using Ansible
======================================================================

This project provides an automated setup for Uptime Kuma, a self-hosted monitoring tool, along with an Nginx web server, Postfix for mail services, and OpenDKIM for secure email signing. The configuration is managed using Ansible, making it easy to deploy and maintain.

Features
--------

-   **Uptime Kuma**: A powerful and easy-to-use monitoring tool, deployed using Docker.
-   **Nginx**: Configured as a reverse proxy with SSL/TLS security enhancements.
-   **Postfix**: Configured as a mail server with support for secure email sending.
-   **OpenDKIM**: Configured for DKIM signing of outgoing emails to improve email deliverability and security.
-   **Certbot**: Automatically obtains and renews SSL certificates from Let's Encrypt.

Requirements
------------

-   A server running Ubuntu 24.04.
-   Ansible installed on your local machine or on the server.
-   A domain name with DNS access to configure necessary records.

Setup Instructions
------------------

### 1\. Clone the Repository

`git clone https://github.com/yourusername/uptime-kuma-nginx-postfix-opendkim.git
cd uptime-kuma-nginx-postfix-opendkim`

### 2\. Update Inventory and Configuration Files

Edit the `hosts` file to include your server's IP address and domain information.

Example:

`[ubuntu_servers]
12.34.56.78 ansible_user=atest`

Update the variables in `main.yaml` with your specific domain and email settings:

`kuma_domain: yourdomain.com
email: youremail@example.com
mail_domain: yourmaildomain.com`

### 3\. Run the Ansible Playbook

Ensure you have SSH access to your server, then run the Ansible playbook:


`ansible-playbook main.yaml -i hosts`

This will install and configure Uptime Kuma, Nginx, Postfix, and OpenDKIM on your server.

### 4\. Configure DNS Records

Once the playbook has been executed, you will need to configure your DNS records for DKIM and SPF. The playbook will provide the necessary DKIM DNS record details, which you can add to your DNS provider.

Example:

-   **DKIM TXT Record**:

    -   **Name**: `mail._domainkey.yourmaildomain.com`
    -   **Value**: `v=DKIM1; k=rsa; p=...`
-   **SPF TXT Record**:

    -   **Name**: `yourmaildomain.com`
    -   **Value**: `v=spf1 mx ~all`

### 5\. Access Uptime Kuma

Once the setup is complete, you can access Uptime Kuma by navigating to `https://yourdomain.com` in your web browser.

Project Structure
-----------------

-   **main.yaml**: The main Ansible playbook that orchestrates the entire setup.
-   **nginx_https.conf.j2**: The Nginx configuration template with SSL/TLS security enhancements.
-   **opendkim.conf.j2**: The OpenDKIM configuration template.
-   **main.cf.j2**: The Postfix configuration template.
-   **hosts**: The Ansible inventory file where you specify your server details.

Contributing
------------

Feel free to fork this project, make improvements, and submit pull requests. Contributions are always welcome!

License
-------

This project is licensed under the MIT License. See the LICENSE file for details.
