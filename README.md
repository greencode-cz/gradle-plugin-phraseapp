# PhraseApp Plugin

client module is a java library which allows you to communicate with the PhraseApp API.

api-gradle is the Gradle plugin which have the client as dependency.

## Tasks

- `phraseappClean` starts task to clean all local resources.
- `phraseappCheck` starts task to check if remote string resources are well formed.
- `phraseappDownload` starts task to download string resources.
- `phraseappUpload` starts task to upload a string resource.

## Parameters

When you want to use this plugin, you need to specify some mandatory parameters and you can customize
the execution of the parameters with optional parameters.

### Mandatory

**Kotlin**

```kotlin
import phraseapp.phraseapp

apply {
    plugin("com.decathlon.phraseapp")
}

phraseapp {
    authToken.set("token <token>")
    projectId.set("<id>>")
    mainLocaleId.set("<id>>")
    resFolders.set(arrayListOf("path_to_res_folder"))
}
```

**Groovy**

```groovy
apply plugin: 'com.decathlon.phraseapp'

phraseapp {
    // Authentication token used to communicate with PhraseApp.
    authToken = 'token <token>'

    // Project id of your PhraseApp project.
    projectId = '<id>'

    // Identifier of the default locale.
    mainLocaleId = '<id>'

    // Target locations to print all translations from PhraseApp.
    resFolders = ['<path_to_res_folder>']
}
```

If one of your resource folder have multiple strings files, you can use `resFoldersMultiStrings`
property:

**Kotlin**
```kotlin
phraseapp {
    resFoldersMultiStrings.set(
        mapOf(
            "${project.projectDir.absolutePath}/src/main/res" 
                    to arrayListOf("strings.xml, strings_2.xml", "strings_3.xml")
        )
    )
}
```

**Groovy**

```groovy
def resFolders = [:]
resFolders.put(
        project.projectDir.absolutePath + '/src/main/res',
        [ "strings.xml", "strings_2.xml", "strings_3.xml" ]
)

phraseapp {
    // mandatory fields...

    resFoldersMultiStrings = resFolders
}
```

### Optional

**Kotlin**

```kotlin
phraseapp {
    // mandatory fields...

    // Generate the output adapted to the platform. Can be 'ANDROID', soon 'IOS' and 'FLUTTER'
    platform.set(phraseapp.internal.Platform.ANDROID)

    // Download the default locale from PhraseApp and write it on the disk with the download task. Default: false.
    overrideDefaultFile.set(false)

    // Phraseapp base url to consume Phraseapp API. Default value: https://api.phraseapp.com/api
    phraseappBaseUrl.set("<base_url>")

    // If you aren't interested by the json file generated by the download task, you don't need to fill this property.
    outputLocation.set("<path_to_location>")

    // If you want to convert a PhraseApp locale to your custom locale, add it into this map.
    // For example: ['zh-CN': 'zh-Hans']
    exceptions.set(mapOf())

    // If you want to convert all placeholder into your platform's placeholder, switch this parameter to true. Default: false.
    placeholder.set(false)

    // If you want to specify your custom locale in the name of a PhraseApp locale, you can specify the regex of your PhraseApp locale name here. Default: .+_([a-z]{2}-[A-Z]{2})
    localeNameRegex.set("<string>")
}
```

**Groovy**

```groovy
phraseapp {
    // mandatory fields...

    // Generate the output adapted to the platform. Can be 'ANDROID', soon 'IOS' and 'FLUTTER'
    platform = '<platform>'

    // Download the default locale from PhraseApp and write it on the disk with the download task. Default: false.
    overrideDefaultFile = false

    // Phraseapp base url to consume Phraseapp API. Default value: https://api.phraseapp.com/api
    phraseappBaseUrl = "<base_url>"

    // If you aren't interested by the json file generated by the download task, you don't need to fill this property.
    outputLocation = "<path_to_location>"

    // If you want to convert a PhraseApp locale to your custom locale, add it into this map.
    // For example: ['zh-CN': 'zh-Hans']
    exceptions = [:]

    // If you want to convert all placeholder into your platform's placeholder, switch this parameter to true. Default: false.
    placeholder = false

    // If you want to specify your custom locale in the name of a PhraseApp locale, you can specify the regex of your PhraseApp locale name here. Default: .+_([a-z]{2}-[A-Z]{2})
    localeNameRegex = "<string>"
}
```

## Download

```kotlin
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("com.decathlon.phrase:phrase-gradle-plugin:<last-version>")
    }
}
```

Snapshots of the development version are available in [Sonatype's `snapshots` repository][snap].

## License

    Copyright 2021 Decathlon.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

[snap]: https://oss.sonatype.org/content/repositories/snapshots/com/decathlon/phrase/
