<h1 align="center"> weather </h1>

<p align="center"> 获取天气预报SDK.</p>

* crackersw/weater

### 安装
```shell
composer require crackersw/weather -vvv
```

### 配置
在使用本扩展之前，你需要去高德开放平台注册账号，然后创建应用，获取应用的API Key。

### 使用
```php
use CrackerSw\Weather\Weather;
$key = "xxxxxxxxxxxxxxxxxxxxx";
$weather = new Weather($key);
```
### 获取实时天气

```php
$response = $weather->getWeather("无锡");
```
返回示例

```json
{
    "status": "1",
    "count": "1",
    "info": "OK",
    "infocode": "10000",
    "lives": [
        {
            "province": "江苏",
            "city": "无锡市",
            "adcode": "320200",
            "weather": "多云",
            "temperature": "28",
            "winddirection": "西",
            "windpower": "≤3",
            "humidity": "40",
            "reporttime": "2022-04-22 13:37:16"
        }
    ]
}
```
### 获取近期天气预报
```php
$response = $weather->getWeather("无锡","all");
```

返回示例

```json
{
    "status": "1",
    "count": "1",
    "info": "OK",
    "infocode": "10000",
    "forecasts": [
        {
            "city": "无锡市",
            "adcode": "320200",
            "province": "江苏",
            "reporttime": "2022-04-22 13:37:16",
            "casts": [
                {
                    "date": "2022-04-22",
                    "week": "5",
                    "dayweather": "多云",
                    "nightweather": "中雨",
                    "daytemp": "30",
                    "nighttemp": "19",
                    "daywind": "南",
                    "nightwind": "南",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2022-04-23",
                    "week": "6",
                    "dayweather": "小雨",
                    "nightweather": "多云",
                    "daytemp": "26",
                    "nighttemp": "16",
                    "daywind": "东南",
                    "nightwind": "东南",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2022-04-24",
                    "week": "7",
                    "dayweather": "多云",
                    "nightweather": "多云",
                    "daytemp": "29",
                    "nighttemp": "18",
                    "daywind": "东南",
                    "nightwind": "东南",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2022-04-25",
                    "week": "1",
                    "dayweather": "暴雨",
                    "nightweather": "小雨",
                    "daytemp": "28",
                    "nighttemp": "21",
                    "daywind": "东南",
                    "nightwind": "东南",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                }
            ]
        }
    ]
}
```
### 获取XML格式返回值
第三个参数为返回值类型，可选`json`与`xml`，默认`json`:
```php
$response = $weather->getWeather("无锡","all","xml");
```
返回示例

```xml
<response>
    <status>1</status>
    <count>1</count>
    <info>OK</info>
    <infocode>10000</infocode>
    <lives type="list">
        <live>
            <province>江苏</province>
            <city>无锡市</city>
            <adcode>320200</adcode>
            <weather>多云</weather>
            <temperature>28</temperature>
            <winddirection>西</winddirection>
            <windpower>≤3</windpower>
            <humidity>40</humidity>
            <reporttime>2022-04-22 13:37:16</reporttime>
        </live>
    </lives>
</response>
```
### 参数说明
```php
array|string getWeather(string $city,$string $type = "base",string $format = "json")
```
* `$city` -城市名，比如："无锡";
* `$type` -返回内容类型：`base`:返回实况天气/ `all`:返回预报天气;
* `$format` -输出数据格式，默认为`json`格式，当output设置为`xml`时，输出的为XML格式数据;

### 在Laravel中使用 
在Laravel中使用也是同样的安装方式，配置写在config/services.php中
```php
    .
    .
    .
    "weather" => [
        "key" => env("WEATHER_API_KEY"),
    ],
```
然后在`.env`中配置`WEATHER_API_KEY`:
```php
WEATHER_API_KEY=xxxxxxxxxxxxxxxxxxxxx
```
可以用两种方式来获取`CrackerSw\Weather\Weather`实例:

**方法参数注入**

```php
    .
    .
    .
    public function getWeather(Weather $weather) 
    {
        $response = $weather->getWeather('无锡');
    }
    .
    .
    .
```

**服务名访问**

```php
    .
    .
    .
    public function getWeather(Weather $weather) 
    {
        $response = app('weather')->getWeather('无锡');
    }
    .
    .
    .
```

## License

MIT