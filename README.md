# localdev-util

A docker compose file that has log ingest and service using [seq](https://datalust.co/) and [seq-gelf](https://github.com/datalust/seq-input-gelf), trace ingest using [tempo](https://grafana.com/oss/tempo/), trace visualisation using [grafana](https://grafana.com/oss/grafana/), and a golang module proxy using [athens](https://docs.gomods.io/).

I wrote a blog post about it here:

## How to use this?

1. clone the repository
2. create an environment variable named `SEQ_PH` in your rc file (`.bashrc`, `.zshrc`, see your choice of shell) and set the value to the output of the following command:
   ```shell
   echo '<password>' | docker run --rm -i datalust/seq config hash
   ```
3. start everything using `docker compose up`
4. try to log into the various things:
   1. grafana: [http://localhost:3998], use `admin` / `admin` first time, and change the password to whatever you would like
   2. seq: [http://localhost:8089](http://localhost:8089), use `admin` for username, and whatever password you created the hash for in step 2
5. connect your services that are running in a separate docker compose:
   1. send GELF logs to `udp://host.docker.internal:12201`
   2. send traces from your trace exporter to `host.docker.internal:6666` using insecure tls

That should be everything.
