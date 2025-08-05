# BTech_B-Group3
A script that generate a daily system health report (disk,memory.cpu.running services). It runs at 9am every morning and result opens in port 8080 on the browser.

DOCUMENTARY 

System Health Dashboard Script – Documentation

Project Purpose

This project aims to monitor the health status of a Linux system by providing:

Disk usage

Memory consumption

System uptime

Running services


The data is output as an HTML dashboard for easy viewing via a web browser, hosted using an nginx Docker container.


---

How to Run the Script

1. Navigate to the project directory:



cd ~/project/web

2. Run the script manually:



./health_report.sh

> Make sure the script is executable:



chmod +x health_report.sh

The output will be saved in the file:

~/project/web/index.html



🧾 Sample Output

Here's an example of what the generated index.html might look like:

<!DOCTYPE html>
<html>
<head><title>System Health Report</title></head>
<body>
<h1>System Health Report - Mon Aug 4 21:09:30 GMT 2025</h1>
<h2>Disk Usage:</h2>
<pre>
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2       233G   13G  209G   6% /
...
</pre>
<h2>Memory Usage:</h2>
<pre>
              total        used        free      shared  buff/cache   available
Mem:           7.5Gi       2.2Gi       3.5Gi       496Mi       2.5Gi       5.3Gi
Swap:          3.7Gi          0B       3.7Gi
</pre>
...
</body>
</html>

> You can open it in your browser at:
http://localhost:8080 or your local IP (e.g., http://10.173.128.203:8080).


How to Schedule the Script with Cron

To run the script automatically at regular intervals:

1. Open the crontab editor:



crontab -e

2. Add this line to run the script every hour:



0 * * * * /home/knoxkiimo/project/web/health_report.sh

> Make sure the script path is correct and it is executable (chmod +x).



To check if cron is running:

systemctl status cron


Docker Setup for Web Hosting

Use Docker to host the generated HTML file with nginx:

1. Run nginx container

sudo docker run -d \
  --name mynginx \
  -p 8080:80 \
  -v /home/knoxkiimo/project/web:/usr/share/nginx/html:ro \
  nginx

-p 8080:80: Exposes port 80 inside the container to port 8080 on your machine.

-v: Mounts your local folder to the container’s web root.


2. View the page in browser

Go to:

http://localhost:8080

Or if you're on a different machine in the same network, use your IP:

http://<your-local-ip>:8080


Requirements

Bash (Linux/macOS terminal)

Docker & Docker daemon (running)

Cron (for automation)