- HTTP/HTTPS 方式下避免每次 push 时都要输入密码的方式：

  - 创建 `git-credentials` 
  
  ```
  touch ~/.git-credentials
  ```
  
  - 给 `.git-credentials` 文件添加内容
  
  ```
  http://{username}:{passwd}@github.com
  ```
  
  - 添加 git 配置
  
  ```
  git config --global credential.helper store
  ```
  
  - 查看 `~/.gitconfig` 文件变化，会出现下面所示的配置项：
  
  ```
  [credential]
    helper = store
  ```
