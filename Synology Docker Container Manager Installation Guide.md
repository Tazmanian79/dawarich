```markdown
# How to Install Dawarich on a Synology NAS with Container Manager

## 1. Create the Directories
- In your `Volume1`, create the directory:
  `docker/dawarich`
- Inside the newly created `dawarich` directory, create the following subdirectories:
  - `db_data`
  - `gem_cache`
  - `public`
  - `shared_data`
    - `watched`

## 2. Set Up the Dawarich Project in Container Manager
1. Open **Container Manager**.
2. Navigate to **Project**.
3. Click **Create**.
   - Name the project: `dawarich`
   - Path: `docker\dawarich`
   - Source: Select **docker-compose.yml** upload
4. **Download** [this file](link-to-docker-compose-file) to your PC.
5. Click **Browse** and select the `docker-compose.yml` file you just downloaded.
6. Click **Next**.

**Note:** Dawarich uses port `3000`.  
If you want to use a different port, modify it **before** clicking **Next**.  
For example, to use port `3030`, change:

```yaml
ports:
  - 3000:3000
```

to:

```yaml
ports:
  - 3030:3000
```

Keep the second `3000` unchanged, as Dawarich always listens on this port.

If you want to access your Dawarich from outside your local network, you have to set up a reverse proxy. You will also need to change the compose.yml file. Before clicking **Next**, go first to point 5.

7. Click **Next**  
8. Click **Complete**

Your Synology NAS will now download and install all necessary files. Depending on your NAS model, this process might take a while. Wait at least 10 minutes to ensure everything is set up correctly. Once done, your project should appear in Container Manager.

## 3. Access Dawarich
Open your browser and go to:  
`http://<ip_of_your_nas>:3000`  
Follow the on-screen instructions to complete the Dawarich setup.

## 4. Updating Dawarich
Since Dawarich is still in beta, expect frequent updates (some may include breaking changes). When an update is available, you will be notified in **Container Manager**. Simply click **Update** and allow the update process to finish. Once it's done, you can log in again and continue using Dawarich.

## 5. How to Set Up a Reverse Proxy
If you want to access your Dawarich from outside your local network, you need to set up a Reverse Proxy. If you don’t know what a reverse proxy is, visit [this guide](link-to-reverse-proxy-guide) for assistance in setting it up.

If you have set up the reverse proxy according to the guide, you only need to add your domain (for example, mynas.mydomain.com) to `compose.yaml`.  
Search for:

```yaml
APPLICATION_HOSTS: localhost
```

And change it to:

```yaml
APPLICATION_HOSTS: localhost,mynas.mydomain.com
```

You need to make this change twice: once for `dawarich_app:` and once for `dawarich_sidekiq:`.

## Credits
The `compose.yaml` file was co-created by Zandhaas from the Synology Forum.
```
