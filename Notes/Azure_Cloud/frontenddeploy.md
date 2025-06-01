for build=----
```
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
   npm install
   npm run build
```

for copy local to vm------

scp -r D:\My_Code\Terraform\VMs\ToDo_frontend\ReactTodoUIMonolith\build adminuser@40.68.229.133:/home/adminuser







on VM
```
    6  sudo apt update
    7  sudo apt install nginx
    8  ls
    9  sudo cp -r /home/adminuser/build/* /var/www/html/
   10  cd /var/www/html/
   11  ls
   12  rm index.nginx-debian.html
   13  sudo rm index.nginx-debian.html
```
