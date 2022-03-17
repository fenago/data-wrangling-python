#### Data Wrangling with Python (Local Setup Guide)

1. Install Docker https://docs.docker.com/get-docker/

2. Pull Lab Environment Image:

`docker pull fenago/data-wrangling-python`

3. Run Lab Environment Image:

`docker run -d --user root -p 80:80 --name wrangling -e GRANT_SUDO=yes -e JUPYTER_ENABLE_LAB=yes fenago/data-wrangling-python jupyter lab --port 80 --allow-root`

*Password:* 1234


Open http://localhost:80 in Chrome browser


**Optional:**

- Restart lab environment: `docker restart wrangling`
- Delete lab environment: `docker stop wrangling  && docker rm wrangling`