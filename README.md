# Kotlin Functional Options

[![Build Status](https://travis-ci.org/peter-tackage/kotlin-options.svg?branch=master)](https://travis-ci.org/peter-tackage/kotlin-options)

Options in Kotlin using sealed classes.

Kotlin has nullable types, however, the use of `null` as a value is not supported in some popular libraries, such as RxJava 2. This means that another way of representing the absence of a value is required.

This mini-library allows you to represent the absence of a value without worrying about nulls and provides functional operators to transform the value.

## Usage:

Create an Option from a nullable type using `optionOf`:
 
```Kotlin
    fun getCurrentUserId() : Option<String> {
        val userId : String? = getUserId() // something which might return null
        return optionOf(value)
    }
```

Transform the value by chaining functional operators as required:

``` Kotlin
    getCurrentUserId()
            .filter { it.isNotEmpty() && it != "Invalid Id" }
            .flatMap { getCurrentUserFromDatabase(it) }
            .map { it.username }
            .map { "Logged in user: $it" }
            .matchAction( { log(it) }, { log("No user to login!") })
```

## Alternatives

The API of this library was inspired by the [Options](https://github.com/tomaszpolanski/Options) library written by [Tomek Polanski](https://twitter.com/tpolansk).

## License

    Copyright 2017 Peter Tackage

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

