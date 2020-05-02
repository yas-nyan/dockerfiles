# gobgpd on docker 

## usage

```shell
# update gobgpd.conf
vi gobgpd.conf 
# build
docker build -t gobgp ./ 
# run
docker run --name gobgp_poc gobgp -d
# exec gobgp command (e.g. show bgp peer)
docker exec -it gobgp_poc gobgp nei
```