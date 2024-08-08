# Securing Docker Containers 

The "Docker_security" project is designed to create a secure Docker environment for an application called "todo-app." This project emphasizes running the application with a non-root user inside Docker containers. Utilizing a non-root user is a critical security best practice, as it helps mitigate the risks associated with containerized applications by limiting the privileges an attacker could exploit. This security measure ensures that even if an attacker manages to exploit vulnerabilities within the container, their ability to cause harm is significantly constrained.

## Project Goals

- **Enhanced Security:** By configuring the application to run with a non-root user, the project adheres to security best practices that minimize the impact of potential security breaches.
- **Reduced Privileges:** Running processes with minimal privileges reduces the risk of unauthorized access and potential damage.
- **Improved Container Management:** Proper setup and configuration of Docker containers enhance the overall stability and security of the application.

## Configuration Instructions

### 1. Modifying the .env File

To begin, configure the environment variables for the Docker containers:

- Locate the `.env` file in the root directory of your project.
- Find the `MY_user` variable in the `.env` file.
- Change the value of `MY_user` to the desired username that you want to use inside the Docker container. For instance, if you choose `myuser`, update the variable accordingly:

  ```
  MY_user=myuser
  ```

### 2. Updating Configuration in src/persistence/sqlite.js

Ensure the SQLite configuration aligns with the username specified in the `.env` file:

- Open the `sqlite.js` file, located in the `src/persistence/` directory.
- Locate the line specifying the file path for SQLite, typically around line 3:

  ```
  const dbPath = '/home/myuser/app/todos/todo.db';
  ```

- Update the file path to reflect the username set in the `.env` file. If you used `newuser` as the username, the updated path should be:

  ```
  const dbPath = '/home/newuser/app/todos/todo.db';
  ```

### Building and Running the Docker Containers

With your configurations in place, you can now build and deploy the Docker containers. Use the following command:

```
docker-compose up --build
```

This command will:

- **Build the Docker Image:** Follow the instructions defined in the Dockerfile to create the Docker image.
- **Start the Containers:** Deploy the containers as specified in the `docker-compose.yml` file.

### Accessing the Application

After the Docker containers are up and running, access the "todo-app" application through your web browser by navigating to the following URL:

```
http://localhost:3000
```

This URL will direct you to the "todo-app" application, now operational within the Docker containers you have configured.

## Additional Considerations

- **Verify Configurations:** Ensure all file paths and environment variables are correctly configured to prevent issues during container setup.
- **Keep Docker Updated:** Regularly update Docker and Docker Compose to leverage the latest features and security updates.
- **Implement Further Security Measures:** Consider additional security practices such as network segmentation and container scanning to enhance the protection of your application and infrastructure, ensuring a secure and reliable environment.

## Best Practices for Docker Security

To maximize security, follow these best practices:

- **Run Containers with Least Privilege:** Always use a non-root user for running applications inside containers.
- **Regularly Update Images:** Keep your Docker images up to date to incorporate security patches and improvements.
- **Limit Container Capabilities:** Use Docker's security options to restrict the capabilities and resources of containers.
- **Enable Docker Content Trust:** Use Docker Content Trust (DCT) to ensure that the images you use are signed and verified.
- **Monitor Container Activity:** Implement monitoring tools to keep an eye on container activity and detect any suspicious behavior.
- **Use a Firewall:** Configure a firewall to control and monitor the traffic to and from your Docker containers.
- **Implement Resource Limits:** Set resource limits on containers to prevent any single container from exhausting the host's resources.
