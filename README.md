# libsigner_uniapp

应用签名-Uniapp 示例程序

## 插件配置

```json
{
  "name": "Signer",
  "id": "Signer",
  "version": "1.0.0",
  "description": "客户端的安全签名工具",
  "_dp_type":"nativeplugin",
  "_dp_nativeplugin":{
    "android": {
      "integrateType": "aar",
      "plugins": [
        {
          "type": "module",
          "name": "Signer",
          "class": "com.github.militch.libsigner_uniplugin.SignerModule"
        }
      ],
      "dependencies": [
        "commons-codec:commons-codec:1.15"
      ],
      "abis": [
        "arm64-v8a"
      ]
    },
    "ios": {
      "integrateType": "framework",
      "plugins": [
        {
          "type": "module",
          "name": "Signer",
          "class": "SignModule"
        }
      ],
      "deploymentTarget": "11.0",
      "validArchitectures": [
        "arm64"
      ],
      "hooksClass": "",
      "frameworks": [],
      "embedFrameworks": [],
      "resources": [],  
      "privacies": [],
      "parameters": {}
    } 
  }  
}
```