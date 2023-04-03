<div id="header" align="center">
  <img src="https://media.giphy.com/media/vLlpbDafjgHystuJ0a/giphy.gif" width="100"/>
  <div>
    <img src="https://komarev.com/ghpvc/?username=PZhukovski&style=flat-square&color=green" alt=""/>
  </div>
</div>
<div align="center">

[![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=PZhukovski&layout=compact&hide=css)](https://github.com/PZhukovski/github-readme-stats)
</div>

### Hi there 👋

---

### :hammer_and_wrench: Languages and Tools :
<div>
 <img src="https://github.com/devicons/devicon/blob/master/icons/css3/css3-plain-wordmark.svg"  title="CSS3" alt="CSS" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/html5/html5-original.svg" title="HTML5" alt="HTML" width="40" height="40"/>&nbsp;
   <img src="https://github.com/devicons/devicon/blob/master/icons/javascript/javascript-original.svg" title="JavaScript" alt="JavaScript" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/react/react-original-wordmark.svg" title="React" alt="React" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/redux/redux-original.svg" title="Redux" alt="Redux " width="40" height="40"/>&nbsp;
   <img src="https://github.com/devicons/devicon/blob/master/icons/typescript/typescript-original.svg" title="Typescript" alt="Typescript" width="40" height="40"/>&nbsp;
   <img src="https://github.com/devicons/devicon/blob/master/icons/webpack/webpack-original.svg" title="Webpack" alt="Webpack" width="40" height="40"/>&nbsp;
        <img src="https://github.com/devicons/devicon/blob/master/icons/git/git-original.svg" title="GIT" alt="GIT" width="40" height="40"/>&nbsp;
    <img src="https://github.com/devicons/devicon/blob/master/icons/materialui/materialui-original.svg" title="Material UI" alt="Material UI" width="40" height="40"/>&nbsp;
     <img src="https://github.com/devicons/devicon/blob/master/icons/eslint/eslint-original.svg" title="ESlint" alt="ESlint" width="40" height="40"/>&nbsp;
     <img src="https://github.com/devicons/devicon/blob/master/icons/tailwindcss/tailwindcss-original-wordmark.svg" title="Tailwind" alt="Tailwind" width="40" height="40"/>&nbsp;
</div>

---
<!--
**PZhukovski/PZhukovski** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->

#### Пример реализации запроса
```php
<?php

$secret = '5a44c5dff55f3c15a4cce8d7c4cc27e207c7e189';
$method = 'POST';
$contentType = 'application/json';
$date = date(DateTimeInterface::RFC2822);
$path = '/v2/origin/custom/f90ba33d-c9d9-44da-b76c-c349b0ecbe41/connect';

$url = "https://amojo.amocrm.ru" . $path;

$body = [
    'account_id' => 'af9945ff-1490-4cad-807d-945c15d88bec',
    'title' => 'ScopeTitle', //Название вашего канала, отображаемое пользователю
    'hook_api_version' => 'v2',
];
$requestBody = json_encode($body);
$checkSum = md5($requestBody);

$str = implode("\\n", [
    strtoupper($method),
    $checkSum,
    $contentType,
    $date,
    $path,
]);

$signature = hash_hmac('sha1', $str, $secret);

$headers = [
    'Date' => $date,
    'Content-Type' => $contentType,
    'Content-MD5' => strtolower($checkSum),
    'X-Signature' => strtolower($signature),
];

$curlHeaders = [];
foreach ($headers as $name => $value) {
    $curlHeaders[] = $name . ": " . $value;
}

echo $method . ' ' . $url . PHP_EOL;
foreach ($curlHeaders as $header) {
    echo $header . PHP_EOL;
}
echo PHP_EOL . $requestBody . PHP_EOL;

$curl = curl_init();
curl_setopt_array($curl, [
    CURLOPT_URL => $url,
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_TIMEOUT => 5,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => $method,
    CURLOPT_POSTFIELDS => $requestBody,
    CURLOPT_HTTPHEADER => $curlHeaders,
]);

$response = curl_exec($curl);
$err = curl_error($curl);
$info = curl_getinfo($curl);
curl_close($curl);
if ($err) {
    $result = "cURL Error #:" . $err;
} else {
    echo "Status: " . $info['http_code'] . PHP_EOL;
    echo $response . PHP_EOL;
}
```
