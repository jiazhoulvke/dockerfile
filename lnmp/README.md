示例:

```bash
docker run -d --name lnmp -p 80:80 -p 3306:3306 -p 22:22 -p 6379:6379 -v ~/Sites:/var/www --restart=always jiazhoulvke:lnmp
```
