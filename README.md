# sonarqube- installation steps 
SonarQube - Docker installation


> Edit the system configuration file  vi /etc/sysctl.conf


> Insert the following lines at the end of this file.
vm.max_map_count=262144
fs.file-max=65536


> Enable the system configuration.
sysctl -p


> Create a configuration file named 99-sonarqube.conf.
vi /etc/security/limits.d/99-sonarqube.conf


> Paste the following lines in the vi editor
root   -   nofile   65536
root   -   nproc    7610


> Reboot the system


> Start the docker service using systemctl start docker
(Note : you need to have docker installed in your system)


Execute the command  
> docker pull sonarqube


> List the docker images



> Create Docker volumes to store the SonarQube persistent data.
> docker volume create sonarqube-conf 
> docker volume create sonarqube-data
> docker volume create sonarqube-logs
> docker volume create sonarqube-extensions


> Verify the persistent data directories.
docker volume inspect sonarqube-conf 

docker volume inspect sonarqube-data
docker volume inspect sonarqube-logs
docker volume inspect sonarqube-extensions

 create symbolic links to an easier access location.


mkdir /sonarqube
ln -s /var/lib/docker/volumes/sonarqube-conf/_data /sonarqube/conf
ln -s /var/lib/docker/volumes/sonarqube-data/_data /sonarqube/data
ln -s /var/lib/docker/volumes/sonarqube-logs/_data /sonarqube/logs
ln -s /var/lib/docker/volumes/sonarqube-extensions/_data /sonarqube/extensions

Start a SonarQube container with persistent data storage.
docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 -v sonarqube-conf:/opt/sonarqube/conf -v sonarqube-data:/opt/sonarqube/data -v sonarqube-logs:/opt/sonarqube/logs -v sonarqube-extensions:/opt/sonarqube/extensions sonarqube



Open your browser by the url  IP address of you server plus:9000

The SonarQube dashboard will be presented.
 
Click on the Login button and use the Sonarqube default username and password.
• Default Username: admin
