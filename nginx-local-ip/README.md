# nginx-local-ip Resources

## default.conf.template

This is a customized version of the nginx configuration with the following changes:

- Avoids setting the `Host` header when proxying since this did not work when connecting to a CHT instance over HTTPS.  (See [this Stack Overflow comment](https://stackoverflow.com/questions/51858725/nginx-proxy-pass-to-https#comment130089536_68767536) for more information.)
- Automatically redirects requests for root (`/`) to `/dbinfo`. This is needed because the exporter checks this endpoint and a CHT instance will not return this JSON data from root (`/`). (Basically, this tricks the exporter into thinking it is connected to a Couch instance when it is actually talking to a CHT instance.)

## entrypoint.sh

This is just a straight copy of the default `entrypoint.sh` from the `nginx-local-ip` repository. (I am not sure why this is not included in the image by default....)
