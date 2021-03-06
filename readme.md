# CNV_EPOS

FANUC ロボット用 KAREL プログラム  
位置レジスタに記録された、ユーザー座標相当の座標値をワールド座標相当の座標値に変換を行います。(またその逆も可能です)

## 概要

位置レジスタは現在選択されている座標系における座標値が記録されるという仕組みです。このため、記録された状態と異なる座標系に切り替えたとき同じレジスタであっても異なる位置をとります。  
当プログラムを使用することで座標系が異なる場合でも、ロボット空間上で同一の姿勢を取ることが可能になります。  
理由あって演算用の座標系と動作用の座標系を分ける場合、後から一括で座標変換を行いたい場合などに有用です。  
また、誤って座標系の設定を行わずに記録してしまった座標の変換を行うことができます。

## 使用方法

TP プログラム内で呼び出して下さい。

### CNV_EPOS_UF0

ある位置レジスタの値がユーザ座標 x で記録されたと仮定して、
ワールド座標相当の座標値に変換を行います。

- 引数 1  
  記録された際のユーザ座標系番号
- 引数 2  
  変換する位置レジスタ番号
- 引数 3  
  変換後出力先位置レジスタ番号

> 1: ﾖﾋﾞﾀﾞｼ CNV_EPOS_UF0(1,1,2)
>
> ユーザー座標番号 1 で記録された位置レジ[1]を、ワールド座標相当値に変換し位置レジ[2]に出力します

### CNV_EPOS_UFX

ある位置レジスタの値がワールド座標で記録されたと仮定して、
ユーザ座標 x 相当の座標値に変換を行います。

- 引数 1  
  変換に使用するユーザ座標系番号
- 引数 2  
  変換する位置レジスタ番号
- 引数 3  
  変換後出力先位置レジスタ番号

> 1: ﾖﾋﾞﾀﾞｼ CNV_EPOS_UFX(1,1,2)
>
> ワールド座標で記録された位置レジ[1]を、ユーザー座標番号 1 相当値に変換し位置レジ[2]に出力します

### 追記

ユーザー座標番号 A からユーザー座標番号 B への変換が必要な場合には下記の様な方法で行なえます。

> 1: ﾖﾋﾞﾀﾞｼ CNV_EPOS_UF0(1,1,2)  
> 2: ﾖﾋﾞﾀﾞｼ CNV_EPOS_UFX(2,2,3)

## 注意点

変換後のロボットの形態は、変換前のデータを参照します。  
また、変換した値については目視で確認した上でシステムの構築を行って下さい。

## License

Released under the Apache 2.0 License.
