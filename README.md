
# Node package for automating *Dahua* :tm: camera initialization

This package provides an automatic way to initialize Dahua :tm: cameras via Puppeteer.

## Usage

### Installation

```sh
npm i dahua_initilizer
```

### Usage

```js
const dahuaInitializer = require('dahua_initializer')
```


```js
dahuaInitializer.initialize(option, camera_config)
```

### Option parameter


***screenshots:*** default `false`

***path:*** default `''` (if ***!screenshots*** the field is ignored)

***headless:*** default `true`

### camera_config parameter

The ***camera_config*** field is a *json* object of the following form:

Camera initialization usually has various configuration screens:
```json
    {
    	"ip": "192.168.1.108",
	"port": 80,
        "screens": [
            Object,
            Object
        ]
    }
```
**ip** defaults to 192.168.1.108 and **port** to 80.

Screen object is an array of actions:
    
```json
    [
	{
	    "action": "click",
	    "selector": "#elementID"
        },
        {
	    "action": "fill",
	    "selector": "#elementID",
	    "text": "HelloWorld"
        },
        {
	    "action": "keypress",
	    "selector": "#elementID",
	    "key": "Enter"
	},
	{
	    "action": "delay",
	    "time": 200
	}
    ]
```
***action***:
	Will be performed sequentially. (**Note!** Before any forwarding to the next dialog complete all your actions.)
  

 - ***click***: Simulate a mouse click event on the element
 - ***fill***: This action expects *text* field. (**Note!** Generally, input element need to be clicked before filling.)
 - ***keypress***: This action expects *key* field. At the present we only support *Enter*. (See Puppeteer docs. If you want to extend it :wink:)
 - ***delay***: This action expects *time* field. Some fields need some time after the action is performed, for example the time synchronization. (*time* in *ms*).

 ### Example
 Complete example of ***camera_config*** for camera model: 

```json
{
  "ip": "192.168.1.108",
  "port": "80",
  "screens": [
    [
      {
        "action" : "click",
        "selector" : "#nation_select"
      },
      {"action" :  "fill",
        "selector": "#nation_select",
        "text" : "Spain"
      },
      {
        "action" : "keypress",
        "selector": "#nation_select",
        "key" : "Enter"
      },
      {
        "action" : "click",
        "selector": "#init_language"
      },
      {
        "action": "click",
        "selector": "#login_permission4 .u-dialog-foot a"
      }
    ],
    [
      {
        "action": "click",
        "selector": "#login_permission1 input[type=checkbox]"
      },
      {
        "action": "click",
        "selector": "#login_permission1 .u-dialog-foot a"
      }
    ],
    [
      {
        "action": "click",
        "selector": "#devinit_time_zone #syncPCBtn"
      },
      {
        "action": "delay",
        "time": 1000
      },
      {
        "action": "click",
        "selector": "#devinit_time_zone .u-dialog-foot a"
      }
    ],
    [
      {
        "action": "click",
        "selector": "#device_init input[name=newpwd]"
      },
      {
        "action": "fill",
        "selector": "#device_init input[name=newpwd]",
        "text": "password"
      },
      {
        "action": "click",
        "selector": "#device_init input[name=newpwdcfm]"
      },
      {
        "action": "fill",
        "selector": "#device_init input[name=newpwdcfm]",
        "text": "password"
      },
      {
        "action": "click",
        "selector": "#device_init #devInit_mail_enable"
      },
      {
        "action": "click",
        "selector": "#device_init .u-dialog-foot a"
      }
    ],
    [
      {
        "action": "click",
        "selector": "#login_permission2 .u-dialog-foot a"
      },
      {
        "action" : "delay",
        "time" : 200
      }
    ],
    [
      {
        "action": "click",
        "selector": "#login_permission3 .u-dialog-foot a"
      },
      {
        "action" : "delay",
        "time" : 200
      }
    ]
  ]
}
```

## Tested cameras


