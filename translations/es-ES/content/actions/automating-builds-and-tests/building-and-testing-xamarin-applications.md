---
title: Crear y probar aplicaciones de Xamarin
intro: Puedes crear un flujo de trabajo de integración contínua (IC) en GitHub Actions para crear y probar tu aplicación de Xamarin.
redirect_from:
  - /actions/guides/building-and-testing-xamarin-applications
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
type: tutorial
topics:
  - CI
  - Xamarin
  - Xamarin.iOS
  - Xamarin.Android
  - Android
  - iOS
shortTitle: Compila & prueba las apps de Xamarin
---

{% data reusables.actions.enterprise-beta %}
{% data reusables.actions.enterprise-github-hosted-runners %}

## Introducción

Esta guía te muestra cómo crear un flujo de trabajo que realice integración contínua (IC) para tu proyecto de Xamarin. El flujo de trabajo que creas te permitirá ver cuándo las confirmaciones de una solicitud de extracción causan la construcción o las fallas de prueba en tu rama por defecto; este enfoque puede ayudar a garantizar que tu código siempre sea correcto.

Para encontrar una lista completa de versiones disponibles de Xamarin SDK en los ejecutores de macOS hospedados en {% data variables.product.prodname_actions %}, consulta la documentación:

* [macOS 10.15](https://github.com/actions/runner-images/blob/main/images/macos/macos-10.15-Readme.md#xamarin-bundles)
* [macOS 11](https://github.com/actions/runner-images/blob/main/images/macos/macos-11-Readme.md#xamarin-bundles)

{% data reusables.actions.macos-runner-preview %}

## Prerrequisitos

Te recomendamos tener un entendimiento básico de Xamarin, .NET Core SDK, Yaml, opciones de configuración de flujo de trabajo y cómo crear un archivo de flujo de trabajo. Para obtener más información, consulta:

- "[Sintaxis de flujo de trabajo para las {% data variables.product.prodname_actions %}](/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions)"
- "[Comenzar con .NET](https://dotnet.microsoft.com/learn)"
- "[Aprende Xamarin](https://dotnet.microsoft.com/learn/xamarin)"

## Crear apps de Xamarin.iOS

El ejemplo siguiente demuestra cómo cambiar las versiones predeterminadas de Xamarin SDK y cómo compilar una aplicación de Xamarin.iOS.

```yaml
name: Build Xamarin.iOS app

on: [push]

jobs:
  build:

    runs-on: macos-latest

    steps:
    - uses: {% data reusables.actions.action-checkout %}
    - name: Set default Xamarin SDK versions
      run: |
        $VM_ASSETS/select-xamarin-sdk-v2.sh --mono=6.12 --ios=14.10

    - name: Set default Xcode 12.3
      run: |
        XCODE_ROOT=/Applications/Xcode_12.3.0.app
        echo "MD_APPLE_SDK_ROOT=$XCODE_ROOT" >> $GITHUB_ENV
        sudo xcode-select -s $XCODE_ROOT

    - name: Setup .NET Core SDK 5.0.x
      uses: {% data reusables.actions.action-setup-dotnet %}
      with:
        dotnet-version: '5.0.x'

    - name: Install dependencies
      run: nuget restore <sln_file_path>

    - name: Build
      run: msbuild <csproj_file_path> /p:Configuration=Debug /p:Platform=iPhoneSimulator /t:Rebuild
```

## Crear apps de Xamarin.Android

El ejemplo siguiente demuestra cómo cambiar las versiones predeterminadas de Xamarin SDK y cómo compilar una aplicación de Xamarin.Android.

```yaml
name: Build Xamarin.Android app

on: [push]

jobs:
  build:

    runs-on: macos-latest

    steps:
    - uses: {% data reusables.actions.action-checkout %}
    - name: Set default Xamarin SDK versions
      run: |
        $VM_ASSETS/select-xamarin-sdk-v2.sh --mono=6.10 --android=10.2

    - name: Setup .NET Core SDK 5.0.x
      uses: {% data reusables.actions.action-setup-dotnet %}
      with:
        dotnet-version: '5.0.x'

    - name: Install dependencies
      run: nuget restore <sln_file_path>

    - name: Build
      run: msbuild <csproj_file_path> /t:PackageForAndroid /p:Configuration=Debug
```

## Especificar una versión de .NET

Para utilizar una versión preinstalada de .NET Core SDK en un ejecutor hospedado en {% data variables.product.prodname_dotcom %}, utiliza la acción `setup-dotnet`. Esta acción encuentra una versión específica de .NET desde el caché de las herramientas en cada ejecutor y agrega los binarios necesarios a `PATH`. Estos cambios persistirán para el recordatorio del job.

La acción `setup-dotnet` es la forma recomendada de utilizar .NET con las {% data variables.product.prodname_actions %}, porque garantiza el comportamiento consistente a través de diversos ejecutores y diversas versiones de .NET. Si estás utilizando un ejecutor auto-hospedado, debes instalar .NET y agregarlo a `PATH`. Para obtener más información, consulta la acción [`setup-dotnet`](https://github.com/marketplace/actions/setup-net-core-sdk).
