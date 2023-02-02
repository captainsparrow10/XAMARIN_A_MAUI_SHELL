# Migracion de Xamarin.Forms a MAUI usando la Shell

### Proyecto Migrado

# Guia

---

- Proyecto usado de ejemplo [PlantLady Sin Migrar](https://github.com/maddymontaquila/PlantLady)
- Proyecto completamente migrado [PlantLady Migrado](https://github.com/maddymontaquila/PlantLady/tree/maui-migrate)

## Paso 1: Reconocimiento de los dispositivos en MAUI

Antes de seguir la documentación, queria ver si usando la shell se presenta los problemas de reconocimiento de los dispositivos como paso con la version non-shell, por lo que decidi examinar la version migrado, encontrando de nuevo un problema con la compatbilidad en android. Este se arregla de la siguiente manera:

- Se va a la carpeta que contiene todo, por si no me entienden, se vera de esta manera:

  ![screen1](https://cdn.discordapp.com/attachments/894620271275827302/1070727092783808633/image.png)

- Vamos a `PlantLady.sln` y pegamos esto:
  ```C#
  Microsoft Visual Studio Solution File, Format Version 12.00
  # Visual Studio Version 17
  VisualStudioVersion = 17.2.32330.571
  MinimumVisualStudioVersion = 10.0.40219.1
  Project("{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}") = "PlantLady.UWP", "PlantLady\PlantLady.UWP\PlantLady.UWP.csproj", "{CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}"
  EndProject
  Project("{9A19103F-16F7-4668-BE54-9A1E7A4F7556}") = "PlantLady.Android", "PlantLady\PlantLady.Android\PlantLady.Android.csproj", "{91D882E4-B049-4F66-9B2C-6AD42966217E}"
  EndProject
  Project("{9A19103F-16F7-4668-BE54-9A1E7A4F7556}") = "PlantLady.iOS", "PlantLady\PlantLady.iOS\PlantLady.iOS.csproj", "{FA46E4C6-623B-4F46-85CB-864D01C0C070}"
  EndProject
  Project("{9A19103F-16F7-4668-BE54-9A1E7A4F7556}") = "PlantLady", "PlantLady\PlantLady\PlantLady.csproj", "{CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}"
  EndProject
  Global
    GlobalSection(SolutionConfigurationPlatforms) = preSolution
      Debug|Any CPU = Debug|Any CPU
      Debug|ARM = Debug|ARM
      Debug|iPhone = Debug|iPhone
      Debug|iPhoneSimulator = Debug|iPhoneSimulator
      Debug|x64 = Debug|x64
      Debug|x86 = Debug|x86
      Release|Any CPU = Release|Any CPU
      Release|ARM = Release|ARM
      Release|iPhone = Release|iPhone
      Release|iPhoneSimulator = Release|iPhoneSimulator
      Release|x64 = Release|x64
      Release|x86 = Release|x86
    EndGlobalSection
    GlobalSection(ProjectConfigurationPlatforms) = postSolution
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|Any CPU.ActiveCfg = Debug|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|ARM.ActiveCfg = Debug|ARM
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|ARM.Build.0 = Debug|ARM
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|ARM.Deploy.0 = Debug|ARM
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|iPhone.ActiveCfg = Debug|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|iPhone.Build.0 = Debug|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|iPhone.Deploy.0 = Debug|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|iPhoneSimulator.ActiveCfg = Debug|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|iPhoneSimulator.Build.0 = Debug|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|iPhoneSimulator.Deploy.0 = Debug|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|x64.ActiveCfg = Debug|x64
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|x64.Build.0 = Debug|x64
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|x64.Deploy.0 = Debug|x64
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|x86.ActiveCfg = Debug|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|x86.Build.0 = Debug|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Debug|x86.Deploy.0 = Debug|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|Any CPU.ActiveCfg = Release|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|Any CPU.Build.0 = Release|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|Any CPU.Deploy.0 = Release|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|ARM.ActiveCfg = Release|ARM
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|ARM.Build.0 = Release|ARM
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|ARM.Deploy.0 = Release|ARM
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|iPhone.ActiveCfg = Release|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|iPhone.Build.0 = Release|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|iPhone.Deploy.0 = Release|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|iPhoneSimulator.ActiveCfg = Release|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|iPhoneSimulator.Build.0 = Release|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|iPhoneSimulator.Deploy.0 = Release|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|x64.ActiveCfg = Release|x64
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|x64.Build.0 = Release|x64
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|x64.Deploy.0 = Release|x64
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|x86.ActiveCfg = Release|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|x86.Build.0 = Release|x86
      {CB144BDB-F56A-4894-AFC6-6293EDA2B9B7}.Release|x86.Deploy.0 = Release|x86
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|Any CPU.ActiveCfg = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|Any CPU.Build.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|Any CPU.Deploy.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|ARM.ActiveCfg = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|ARM.Build.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|ARM.Deploy.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|iPhone.ActiveCfg = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|iPhone.Build.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|iPhone.Deploy.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|iPhoneSimulator.ActiveCfg = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|iPhoneSimulator.Build.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|iPhoneSimulator.Deploy.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|x64.ActiveCfg = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|x64.Build.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|x64.Deploy.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|x86.ActiveCfg = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|x86.Build.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Debug|x86.Deploy.0 = Debug|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|Any CPU.ActiveCfg = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|Any CPU.Build.0 = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|Any CPU.Deploy.0 = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|ARM.ActiveCfg = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|ARM.Build.0 = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|ARM.Deploy.0 = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|iPhone.ActiveCfg = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|iPhone.Build.0 = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|iPhone.Deploy.0 = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|iPhoneSimulator.ActiveCfg = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|iPhoneSimulator.Build.0 = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|iPhoneSimulator.Deploy.0 = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|x64.ActiveCfg = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|x64.Build.0 = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|x64.Deploy.0 = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|x86.ActiveCfg = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|x86.Build.0 = Release|Any CPU
      {91D882E4-B049-4F66-9B2C-6AD42966217E}.Release|x86.Deploy.0 = Release|Any CPU
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|Any CPU.ActiveCfg = Debug|Any CPU
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|ARM.ActiveCfg = Debug|iPhone
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|ARM.Build.0 = Debug|iPhone
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|ARM.Deploy.0 = Debug|iPhone
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|iPhone.ActiveCfg = Debug|iPhone
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|iPhone.Build.0 = Debug|iPhone
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|iPhone.Deploy.0 = Debug|iPhone
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|iPhoneSimulator.ActiveCfg = Debug|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|iPhoneSimulator.Build.0 = Debug|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|iPhoneSimulator.Deploy.0 = Debug|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|x64.ActiveCfg = Debug|Any CPU
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|x64.Build.0 = Debug|Any CPU
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|x64.Deploy.0 = Debug|Any CPU
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|x86.ActiveCfg = Debug|Any CPU
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|x86.Build.0 = Debug|Any CPU
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Debug|x86.Deploy.0 = Debug|Any CPU
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|Any CPU.ActiveCfg = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|Any CPU.Build.0 = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|Any CPU.Deploy.0 = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|ARM.ActiveCfg = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|ARM.Build.0 = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|ARM.Deploy.0 = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|iPhone.ActiveCfg = Release|iPhone
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|iPhone.Build.0 = Release|iPhone
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|iPhone.Deploy.0 = Release|iPhone
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|iPhoneSimulator.ActiveCfg = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|iPhoneSimulator.Build.0 = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|iPhoneSimulator.Deploy.0 = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|x64.ActiveCfg = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|x64.Build.0 = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|x64.Deploy.0 = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|x86.ActiveCfg = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|x86.Build.0 = Release|iPhoneSimulator
      {FA46E4C6-623B-4F46-85CB-864D01C0C070}.Release|x86.Deploy.0 = Release|iPhoneSimulator
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|Any CPU.ActiveCfg = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|Any CPU.Build.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|Any CPU.Deploy.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|ARM.ActiveCfg = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|ARM.Build.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|ARM.Deploy.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|iPhone.ActiveCfg = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|iPhone.Build.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|iPhone.Deploy.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|iPhoneSimulator.ActiveCfg = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|iPhoneSimulator.Build.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|iPhoneSimulator.Deploy.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|x64.ActiveCfg = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|x64.Build.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|x64.Deploy.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|x86.ActiveCfg = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|x86.Build.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Debug|x86.Deploy.0 = Debug|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|Any CPU.ActiveCfg = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|Any CPU.Build.0 = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|Any CPU.Deploy.0 = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|ARM.ActiveCfg = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|ARM.Build.0 = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|ARM.Deploy.0 = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|iPhone.ActiveCfg = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|iPhone.Build.0 = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|iPhone.Deploy.0 = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|iPhoneSimulator.ActiveCfg = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|iPhoneSimulator.Build.0 = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|iPhoneSimulator.Deploy.0 = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|x64.ActiveCfg = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|x64.Build.0 = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|x64.Deploy.0 = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|x86.ActiveCfg = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|x86.Build.0 = Release|Any CPU
      {CC55A327-2B7F-4D80-8DAF-B4E0106D1D00}.Release|x86.Deploy.0 = Release|Any CPU
    EndGlobalSection
    GlobalSection(SolutionProperties) = preSolution
      HideSolutionNode = FALSE
    EndGlobalSection
    GlobalSection(ExtensibilityGlobals) = postSolution
      SolutionGuid = {9B906403-1E3A-40CA-AED7-4375E6E15278}
    EndGlobalSection
  EndGlobal
  ```

## Paso 2: Verificación de las carpetas

---

Deberian apreciar 4 carpetas de ejemplo como mostrare a continuación:

- Me refiero lo que esta dentro de la carpeta `PlantLady`, que tendra el mismo nombre de su proyecto
  ![screen2](https://cdn.discordapp.com/attachments/894620271275827302/1070728032538591323/image.png)
- El lado bueno, es que las unicas carpetas que se modificaran seran como el [proyecto anterior](https://github.com/captainsparrow10/XAMARIN_A_MAUI_NON_SHELL/tree/main), denle un vistazo para que entiendan mejor de lo que hablo.
- Aqui nos enfocaremos en la main `PlantLady`, `PlantLady.Android` y `PlantLady.iOS`.

## Paso 3: Actualización de los archivos csproj

---

Iremos a los archivos csproj de cada carpeta que mencione anteriormente ( `PlantLady`, `PlantLady.Android` y `PlantLady.iOS`) y colocaremos lo siguiente:

- `PlantLady`:

  ```C#
  <Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
      <TargetFrameworks>net6.0-ios;net6.0-android</TargetFrameworks>
      <UseMaui>True</UseMaui>
      <OutputType>Library</OutputType>
      <ImplicitUsings>enable</ImplicitUsings>
      <!-- Required for C# Hot Reload -->
      <UseInterpreter Condition="'$(Configuration)' == 'Debug'">True</UseInterpreter>
      <SupportedOSPlatformVersion Condition="'$(TargetFramework)' == 'net6.0-ios'">15.4</SupportedOSPlatformVersion>
      <SupportedOSPlatformVersion Condition="'$(TargetFramework)' == 'net6.0-android'">31.0</SupportedOSPlatformVersion>
    </PropertyGroup>
    <ItemGroup>
      <MauiFont Include="Resources\*" />
    </ItemGroup>
  </Project>
  ```

- `PlantLady.Android`:

  ```C#
  <Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
      <UseMaui>true</UseMaui>
      <TargetFramework>net6.0-android</TargetFramework>
      <OutputType>Exe</OutputType>
        <ImplicitUsings>enable</ImplicitUsings>
      <SupportedOSPlatformVersion Condition="'$(TargetFramework)' == 'net6.0-android'">31.0</SupportedOSPlatformVersion>
    </PropertyGroup>
      <PropertyGroup>
      <UseInterpreter Condition="$(TargetFramework.Contains('-android'))">True</UseInterpreter>
      <SupportedOSPlatformVersion>28.0</SupportedOSPlatformVersion>
    </PropertyGroup>

  <ItemGroup>
      <ProjectReference Include="..\PlantLady\PlantLady.csproj">
        <Project>{EA278C7F-74CB-4DD9-9407-D2FB485A7932}</Project>
        <Name>PlantLady</Name>
      </ProjectReference>
    </ItemGroup>

    <ItemGroup>
      <AndroidResource Include="Resources\layout\Tabbar.xml" />
      <AndroidResource Include="Resources\layout\Toolbar.xml" />
      <AndroidResource Include="Resources\values\styles.xml" />
      <AndroidResource Include="Resources\values\colors.xml" />
      <AndroidResource Include="Resources\mipmap-anydpi-v26\icon.xml" />
      <AndroidResource Include="Resources\mipmap-anydpi-v26\icon_round.xml" />
      <AndroidResource Include="Resources\mipmap-hdpi\icon.png" />
      <AndroidResource Include="Resources\mipmap-hdpi\launcher_foreground.png" />
      <AndroidResource Include="Resources\mipmap-mdpi\icon.png" />
      <AndroidResource Include="Resources\mipmap-mdpi\launcher_foreground.png" />
      <AndroidResource Include="Resources\mipmap-xhdpi\icon.png" />
      <AndroidResource Include="Resources\mipmap-xhdpi\launcher_foreground.png" />
      <AndroidResource Include="Resources\mipmap-xxhdpi\icon.png" />
      <AndroidResource Include="Resources\mipmap-xxhdpi\launcher_foreground.png" />
      <AndroidResource Include="Resources\mipmap-xxxhdpi\icon.png" />
      <AndroidResource Include="Resources\mipmap-xxxhdpi\launcher_foreground.png" />
    </ItemGroup>
  </Project>
  ```

- `PlantLady.iOS`:

  ```C#
  <Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
      <UseMaui>true</UseMaui>
      <TargetFramework>net6.0-ios</TargetFramework>
      <OutputType>Exe</OutputType>
        <ImplicitUsings>enable</ImplicitUsings>
    </PropertyGroup>

    <!-- <ItemGroup>
    <InterfaceDefinition Include="Resources\LaunchScreen.storyboard" />
    </ItemGroup>  -->

    <ItemGroup>
      <ProjectReference Include="..\PlantLady\PlantLady.csproj">
        <Project>{EA278C7F-74CB-4DD9-9407-D2FB485A7932}</Project>
        <Name>PlantLady</Name>
      </ProjectReference>
    </ItemGroup>
  </Project>
  ```

## Paso 3: Actualizar Codigo

---

Aqui reempplazaremos todo lo que tiene que ver con `Xamarin` con `Maui`

- Iremos a la carpeta `PlantLady`:

  ![screen3](https://cdn.discordapp.com/attachments/894620271275827302/1070734701117055076/image.png)

  - Crearemos el archivo `MauiProgram.cs` y colocaremos esto :

    ```C#
    namespace PlantLady;
    public static class MauiProgram
    {
      public static MauiApp CreateMauiApp()
      {
        var builder = MauiApp.CreateBuilder();
        builder
          .UseMauiApp<App>()
          .ConfigureFonts(fonts =>
          {
            fonts.AddFont("AmaticSC-Regular.ttf", "Amatic");
                    fonts.AddFont("materialdesignicons-webfont.ttf","MaterialIcons");
                    fonts.AddFont("Michella-Garden.otf", "Michella");
          });

        return builder.Build();
      }
    }
    ```

  - En `App.xaml` y `AppShell.xaml`, verificaremos que en la parte superior, donde se mencione a Xamarin `xmlns="http://xamarin.com/schemas/2014/forms"` se ponga a Maui usando esto `xmlns="http://schemas.microsoft.com/dotnet/2021/maui"`

  - En `App.xaml.cs` y `AppShell.xaml.xs`, tendremos que reemplazar las siguientes lineas
    `using Xamarin.Forms` y `using Xamarin.Forms.Xaml` por `using Microsoft.Maui;`

  - En `AssemblyInfo.cs`, pondremos solo lo siguiente:
    ```C#
    using Microsoft.Maui;
    [assembly: XamlCompilation(XamlCompilationOptions.Compile)]
    ```
  - Luego vamos a la carpeta `Views` para arreglar ciertos errores presentados en cada archivo:

    - `HomePage.xaml`:
      ```C#
      <?xml version="1.0" encoding="utf-8" ?>
      <ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
                  xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                  x:Class="PlantLady.HomePage"
                  BackgroundColor="{StaticResource LightGreen}">
          <StackLayout>
              <Frame HasShadow="True"
                    HeightRequest="120"
                    WidthRequest="120">
                    <!-- maui bug : https://github.com/dotnet/maui/issues/5812  -->
                  <!-- <Frame.Background>
                      <LinearGradientBrush StartPoint="0,0"
                                  EndPoint="0,1">
                          <GradientStop Color="{StaticResource DarkestGreen}"
                                Offset="0.1"/>
                          <GradientStop Color="{StaticResource DarkGreen}"
                                Offset="1.0"/>
                      </LinearGradientBrush>
                  </Frame.Background> -->
                  <Label Text="Plant Care"
                        Style="{StaticResource HeaderLabel}"
                        HorizontalOptions="CenterAndExpand"
                        VerticalOptions="End"/>
              </Frame>
              <CarouselView>
                  <CarouselView.ItemsSource>
                      <x:Array Type="{x:Type x:String}">
                          <x:String>aloe vera</x:String>
                          <x:String>dracaena</x:String>
                          <x:String>jade</x:String>
                          <x:String>dieffenbachia</x:String>
                          <x:String>dieffenbachia</x:String>
                      </x:Array>
                  </CarouselView.ItemsSource>
                  <CarouselView.ItemTemplate>
                      <DataTemplate>
                          <StackLayout>
                              <Frame HasShadow="True"
                                    CornerRadius="20"
                                    Margin="20"
                                    HeightRequest="300"
                                    WidthRequest="300"
                                    HorizontalOptions="Center"
                                    VerticalOptions="CenterAndExpand">
                                  <Grid ColumnDefinitions="*,*" RowDefinitions="*,200,20,10">
                                      <Label Text="{Binding .}"
                                            Style="{StaticResource PlantLabel}"
                                            Grid.Row="0" Grid.ColumnSpan="2"/>
                                      <Image Source="https://secure.img1-fg.wfcdn.com/im/94669473/resize-h800%5Ecompr-r85/1248/124805864/Live+Aloe+Plant+in+Pot.jpg"
                                            Aspect="AspectFit"
                                            HeightRequest="150"
                                            WidthRequest="150"
                                            Grid.Row="1" Grid.ColumnSpan="2" />
                                      <!--<Label Text="Sun"
                                            HorizontalOptions="Center"
                                            Grid.Row="2" Grid.Column="0" />-->
                                      <AbsoluteLayout Scale=".04" Grid.Row="2" Grid.Column="0" Padding="0" Margin="0,0,15,10">
                                          <Path Data="M377.139 259.492c0 66.637-54.020 120.658-120.658 120.658-66.637 0-120.658-54.021-120.658-120.658 0-66.637 54.020-120.658 120.658-120.658 66.637 0 120.658 54.020 120.658 120.658z" Fill="#000000" />
                                          <Path Data="M228.352 100.669l30.27-77.906 25.979 77.906z" Fill="#000000" />
                                          <Path Data="M228.352 411.341l30.27 77.895 25.979-77.895z" Fill="#000000" />
                                          <Path Data="M100.659 287.601l-77.895-30.29 77.895-25.959z" Fill="#000000" />
                                          <Path Data="M411.361 287.601l77.875-30.29-77.875-25.959z" Fill="#000000" />
                                          <Path Data="M126.597 165.703l-33.659-76.472 73.442 36.7z" Fill="#000000" />
                                          <Path Data="M346.276 385.423l76.524 33.639-36.741-73.442z" Fill="#000000" />
                                          <Path Data="M168.499 388.199l-76.493 33.639 36.72-73.442z" Fill="#000000" />
                                          <Path Data="M388.199 168.499l33.618-76.513-73.4 36.751z" Fill="#000000" />
                                      </AbsoluteLayout>
                                      <StackLayout Orientation="Horizontal" HorizontalOptions="Center" Grid.Row="3" Grid.Column="0" >
                                          <Ellipse Fill="#081C15" />
                                          <Ellipse Fill="#081C15"/>
                                          <Ellipse Fill="#081C15"/>
                                      </StackLayout>
                                      <Label Text="Water"
                                            HorizontalOptions="Center"
                                            Grid.Row="2" Grid.Column="1"
                                            MaxLines="5"
                                            LineBreakMode="TailTruncation" />
                                      <StackLayout Orientation="Horizontal" HorizontalOptions="Center" Grid.Row="3" Grid.Column="1" >
                                          <Ellipse Fill="#081C15" />
                                          <Ellipse />
                                          <Ellipse />
                                      </StackLayout>
                                  </Grid>
                              </Frame>
                          </StackLayout>
                      </DataTemplate>
                  </CarouselView.ItemTemplate>
              </CarouselView>
          </StackLayout>
      </ContentPage>
      ```
    - `HomePage.xaml.cs`, se remueve la linea que menciona a xamarin `using Xamarin.Forms`

    - `PlantsPage.xaml`, se cambia la linea de `xmlns="http://xamarin.com/schemas/2014/forms"` por `xmlns="http://schemas.microsoft.com/dotnet/2021/maui"`

    - `PlantsPage.xaml.cs`, se cambian las lineas de `using Xamarin.Forms` y `using Xamarin.Forms.Xaml` por `using Microsoft.Maui`

- En `PlantLady.Android`, haremos lo siguiente:

  - Crearemos el archivo `MainApplication.cs` y pegaremos lo siguiente :

    ```C#
    using System;
    using Android.App;
    using Android.Runtime;
    using Microsoft.Maui;
    using Microsoft.Maui.Hosting;
    using PlantLady;

    namespace PlantLady.Droid
    {

      [Application]
      public class MainApplication : MauiApplication
      {
        public MainApplication(IntPtr handle, JniHandleOwnership ownership)
          : base(handle, ownership)
        {
        }
        protected override MauiApp CreateMauiApp() => MauiProgram.CreateMauiApp();
      }
    }
    ```

  - En `MainActivity.cs` lo dejaremos de la siguiente manera:

    ```C#
    using System;
    using Microsoft.Maui;
    using Android.App;
    using Android.Content.PM;
    using Android.Runtime;
    using Android.Views;
    using Android.Widget;
    using Android.OS;

    namespace PlantLady.Droid
    {
        [Activity(Label = "PlantLady", Icon = "@mipmap/icon", Theme = "@style/MainTheme", MainLauncher = true, ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation | ConfigChanges.UiMode | ConfigChanges.ScreenLayout | ConfigChanges.SmallestScreenSize )]
        public class MainActivity : MauiAppCompatActivity
        {
            protected override void OnCreate(Bundle savedInstanceState)
            {
                base.OnCreate(savedInstanceState);
            }
        }
    }
    ```

  - Iremos a `Resources` y eliminaremos el archivo `Resource.designer.cs`.

  - Iremos a `Properties`,

    - En `AndroidManifest.xml`, cambiaremos la siguiente linea `<uses-sdk android:minSdkVersion="21" android:targetSdkVersion="29" />` por esta `<uses-sdk android:minSdkVersion="25" android:targetSdkVersion="31" />`

    - En `AssemblyInfo.cs`, lo eliminaremos o comentaran todo su contenido.

- En `PlantLady.iOS`, haremos lo siguiente:

  - En la carpeta `Properties`, en el archivo `AssemblyInfo.cs`, lo eliminaremos o comentaremos todo su contenido.

  - En el archivo `AppDelegate.cs`, lo dejaremos de la siguiente manera:

    ```C#
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using Microsoft.Maui;
    using Foundation;
    using UIKit;

    namespace PlantLady.iOS
    {
        [Register("AppDelegate")]
        public partial class AppDelegate : MauiUIApplicationDelegate
        {
            protected override MauiApp CreateMauiApp() => MauiProgram.CreateMauiApp();
        }
    }
    ```

  - En `Info.plist`, cambiaremos la linea:
    ```C#
    <key>MinimumOSVersion</key>
    <string>8.0</string>
    ```
    Por esta
    ```C#
    <key>MinimumOSVersion</key>
    <string>15.4</string>
    ```
  - Por ultimo, en el `Main.cs` pegaremos lo siguiente:

    ```C#
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using Foundation;
    using UIKit;

    namespace PlantLady.iOS
    {
        public class Application
        {
            static void Main(string[] args)
            {
                UIApplication.Main(args, null,  typeof(AppDelegate));
            }
        }
    }
    ```

## Paso 4: Actualizacion de los nugets

---

- Eliminar `Xamarin.Forms` y `Xamarin.Essentials ` de las nuget references.
- Reemplazar `Xamarin.Community Toolkit` con la ultima versión de `.NET MAUI Community Toolkit`
- Reemplazar `SkiaSharp` con su ultima versión:
  - [SkiaSharp.Views.Maui.Controls](https://www.nuget.org/packages/SkiaSharp.Views.Maui.Controls/2.88.0-preview.232)
  - [SkiaSharp.Views.Maui.Core](https://www.nuget.org/packages/SkiaSharp.Views.Maui.Core/2.88.0-preview.232)
  - [SkiaSharp.Views.Maui.Controls.Compatibility](https://www.nuget.org/packages/SkiaSharp.Views.Maui.Controls.Compatibility/2.88.0-preview.232)
