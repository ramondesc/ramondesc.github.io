---
title: "Adicionando uma splash screen em um aplicativo Android"
date: 2020-03-30T00:46:37-03:00
draft: false
---

{{< figure src="/photo-1585060544812-6b45742d762f.webp" class="" alt="Celular com tela em branco." title="Quando você vê esta tela, o que acha que está acontecendo? Está carregando? Travou? O que você faria?" >}}

Quando criamos aplicativos mobile, precisamos fazer com que as pessoas sintam que estão no controle o tempo todo. Caso você entregue uma tela em branco padrão, eles podem supor que sua aplicação travou.

Minha primeira tentativa de desenvolver aplicações mobile foi com o Flutter. Enquanto pesquisava e aprendia a linguagem encontrei  este [package de Dart](https://pub.dartlang.org/packages/splashscreen). Mas isto é uma route executada antes de aplicação mostrar sua tela principal. Ele pode ser útil caso você queira entregar uma distração positiva ao usuário enquanto carrega o aplicativo. Mas a tela branca continua logo após abrir o aplicativo.

Para definir uma splash screen no Android, é necessário criar nativamente. 

Primeiro, precisamos ir ao arquivo manifesto. Ele contém informações utilizadas pelo sistemas antes da aplicação executar seu código nativo.

Em **android/src/main/AndroidManifest.xml** há uma activity com o seguinte atributo:

```xml
 android:theme="@style/LaunchTheme"
```

O LaunchTheme é encontrado em **android/src/main/res/values/styles.xml**:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <style name="LaunchTheme" parent="@android:style/Theme.Black.NoTitleBar">
        <!-- Show a splash screen on the activity. Automatically removed when
             Flutter draws its first frame -->
        <item name="android:windowBackground">@drawable/launch_background</item>
    </style>
</resources>
```

E a tela em branco é encontrada em **android/src/main/res/drawable/launch_background.xml**:

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- Modify this file to customize your launch splash screen -->
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@android:color/white" />

    <!-- You can insert your own image assets here -->
    <!-- <item>
        <bitmap
            android:gravity="center"
            android:src="@mipmap/launch_image" />
    </item> -->
</layer-list>
```

Agora é necessário adicionarmos a imagem para o endereço de origem. Substitua o launch_image pelo nome da imagem sem a extensão. O resultado será a imagem centralizada na tela com o restante preenchido na cor branca.

Eu necessitava de uma maneira de preencher a tela com uma cor de fundo igual ao da imagem. A solução que encontrei foi editar o item para apontar uma cor diferente. O código final ficou assim:

```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">

    <item>
        <color android:color="#93aeff"></color>
    </item>

    <item>
        <bitmap
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:gravity="center"
            android:src="@drawable/launch_image" />
    </item>

</layer-list>
```

E o resultado visual foi:

{{< figure src="/145649.webp" class="" alt="Uma ilustração de pessoas sobre aviões de papel. O plano de fundo é uniforme com uma mesma cor." >}}

Obrigado por ler até o final. Caso eu tenha cometido qualquer erro, avise-me.

## Referências

- [Right Way to Create Splash Screen on Android](https://android.jlelse.eu/right-way-to-create-splash-screen-on-android-e7f1709ba154)

## Imagens

- [Business vector created by freepik - www.freepik.com](https://www.freepik.com/free-vector/leadership-concept-paper-planes_3165533.htm)
- [Blank phone screen by Pexels](https://images.pexels.com/photos/336948/pexels-photo-336948.jpeg?auto=compress&cs=tinysrgb&h=650&w=940)