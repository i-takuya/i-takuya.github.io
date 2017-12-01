## chef vs ansible　極彩色の大決戦

Puppetも触ろうとしたがおもったよりチュートリアルがイケてなくて断念。

ただざっとドキュメントを見た感じわざわざPuppetを今導入する理由はあんまりない気がする
主な理由は習得難易度。独自DSL及びs/cのアーキテクチャでは複雑と言われているchefよりも簡単に使用できる感あんまりしない。

### 比較表

| プロダクト | Chef        | ansible     |
|-------|--------|---------|
| 会社       | Chef        | Redhat      |
| Deploy方法 | agent       | ssh         |
| 言語       | Ruby DSL    | yaml        |
| 導入難易度 | high        | middle      |
| 情報量     | normal      | too much    |
| チュートリアル   | ええぞ      | 普通        |
| sudo   | chef-clientのみ      | 全部        |
| 表現力 | めちゃたか | yamlの限界 |

### ansible tower導入方法

```
// image pull
docker pull ybalt/ansible-tower
// docker run
docker run -d -p 443:443 --name tower ybalt/ansible-tower
// access to ui
https://localhost
```

### playbook
https://gitlab.com/i-takuya/ansible_mac

playbookはscmからpullできる。

inventoriesなどはuiから登録しなければならない空気を感じる。
```tower-cli```経由なら管理できそうな予感(http://tower-cli.readthedocs.io/en/latest/api_ref/resources/inventory.html)

tower-cli経由で動作させるなら結構便利だなという気がしてきた。

### セキュリティについて

chefはchef-clientのみをsudoersで許可すれば良いがansibleは```ssh <user>@<ip> command```
なので更新系のコマンドは基本的にすべてsudoでの実行が想定される。

そのため基本的に```ALL```で許可する必要があり、アカウントがハックされると言うことはroot権限をとられることと同意である。これを許容できるかは使用する環境次第だろう。

### 表現力について

ansibleは所詮はyamlよ。roleとかgalaxyとか色々用意しているけど、複雑なケースのrole分けや環境ごとの違いなどを吸収するのはChefやPuppetに比べて難しい。・・・気がする。

