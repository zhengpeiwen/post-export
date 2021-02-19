# post请求导出文件

## 代码
```
import axios from 'axios';
export function exportFileUtils(params, url, filename) {
  axios({
    method: 'post',
    withCredentials: true,
    url: url, // 请求地址
    data: params,
    responseType: 'blob', // 防止导出文件破损或乱码
    headers: {
      'Content-Type': 'application/json',
      'x-auth-token': userInfo.token, // 请求token
      'x-project-id': userInfo.projectId  //项目id  
      }
  }).then((res) => {
    try {
      var blob = new Blob([res.data]);
      // var filename = '导出文件.xlsx'; //  文件名字
      var a = document.createElement('a');
      var url = window.URL.createObjectURL(blob);
      a.href = url;
      a.download = filename || '';
      var body = document.getElementsByTagName('body')[0];
      body.appendChild(a);
      a.click();
      body.removeChild(a);
      window.URL.revokeObjectURL(url);
    } catch (e) {}
  });
}
```
