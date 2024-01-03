To install the latest version of Node.js on Ubuntu, you can use the NodeSource repository, which provides the most up-to-date versions of Node.js. Here are the steps:

1. **Add the NodeSource Repository:**

   Open a terminal and run the following commands to add the NodeSource repository to your system:

   ```bash
   curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
   ```

   This command fetches the setup script and executes it.

2. **Install Node.js:**

   Once the repository is added, install Node.js by running:

   ```bash
   sudo apt-get install -y nodejs
   ```

   This command installs Node.js and npm (Node Package Manager).

3. **Verify Installation:**

   Check if Node.js and npm were installed successfully by running:

   ```bash
   node -v
   npm -v
   ```

   This should display the installed Node.js version and npm version.

That's it! You've successfully installed the latest version of Node.js on your Ubuntu system. Keep in mind that you can replace `setup_lts.x` in the first command with `setup_current.x` if you want to install the latest current version of Node.js instead of the LTS version.

Optional: If you encounter permission issues when using npm to install global packages without sudo, you can configure npm to use a directory in your home directory. To do this, follow these steps:

1. Create a directory for global packages in your home directory:

   ```bash
   mkdir ~/.npm-global
   ```

2. Configure npm to use this directory:

   ```bash
   npm config set prefix '~/.npm-global'
   ```

3. Add the following line to your `~/.bashrc` or `~/.zshrc` file to include the new directory in your `PATH`:

   ```bash
   export PATH=~/.npm-global/bin:$PATH
   ```

   Then, run:

   ```bash
   source ~/.bashrc   # or source ~/.zshrc for Zsh users
   ```

This ensures that global npm packages are installed in your home directory without requiring sudo.





To install mongodb follow below url 

https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/

```
use admin
```
```
db.createUser({
  user: "MONGODB_USERNAME",
  pwd: "MONGODB_PASSWORD",
  roles: [
    { role: "readWriteAnyDatabase", db: "admin" },
    { role: "dbAdminAnyDatabase", db: "admin" },
    { role: "userAdminAnyDatabase", db: "admin" }
  ]
})
```

```
mongosh -u "MONGODB_USERNAME" -p "MONGODB_PASSWORD"
```

```
db.grantRolesToUser("MONGODB_USERNAME", [
  { role: "readWriteAnyDatabase", db: "admin" },
  { role: "dbAdminAnyDatabase", db: "admin" },
  { role: "userAdminAnyDatabase", db: "admin" },
  { role: "clusterAdmin", db: "admin" }
])
```
