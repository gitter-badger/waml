# WAML (draft-0.2)

**Notice**: WAML is currently in a very early draft version. Feel free to create a pull request in case of useful suggestions.

Refer to the [changelog] for recent notable changes and modifications.


## Abstract

Web Automation Markup Language (WAML) is definition of action sequences which can be performed on web resources (e.g. regular web pages) within a context of a web browser to simulate user behavior. The WAML specification defines an application of [YAML 1.2] which allows an expirienced user to create a human and machine readable sequence at one go, reuse sequences in any order, and perform context dependent actions.


## Terminology

The underlying format for WAML is YAML so that it inherits all its benefits such as hosting of multiple document within one stream. A WAML stream may contain multiple _scenarios_. Every _scenario_ must be represented by a set of _metadata_ as well as sequence of _actions_ to execute. Every _action_ must have at least one _criteria_ which is represented as _scalar_ (string, integer, etc.) value or a _mapping_.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119].


## Schema

WAML is based on [JSON Schema] that lives at [waml-schema.org]. WAML schema is available in [YAML][waml-yaml] and [JSON][waml-json] formats. A scenario within a WAML stream may define the preferred schema version by defining ```$schema``` property, otherwise a default parser schema is used.


## Scenario Schema

A very basic scenario must contain a ```name``` and ```steps``` property. The list of actions may be empty, however, it is reasonable to have at least one action.

{{ includeScenario('./sources/examples/scenario/simple-scenario.yaml') }}

This minimal example demonstrates the simplicity of WAML. The full list of supported metadata is depicted below.

{{ schema2md('./sources/schema/scenario-schema.yaml') }}

Using this properties, the following more comprehensive example can be created:

{{ includeScenario('./sources/examples/scenario/full-featured-scenario.yaml') }}


## Step Schema

The steps property must be represented as a sequence of actions. Every step represents the smallest identifiable user action.

{{ schema2md('./sources/schema/step-schema.yaml') }}


## Fragment Scenarios

Fragment scenarios can not be executed independently but can only be used in ```include``` actions of other scenarios or fragments.

{{ includeScenario('./sources/examples/scenario/fragment-scenario.yaml') }}


## Actions and Criteria
### Open
#### Open Step Schema

Like for a real user, ```open``` is often the very first action of a scenarios. It triggers the navigation to a particular URL inside the web browser.

{{ schema2md('./sources/schema/steps/open-step-schema.yaml') }}

#### Open Criteria Schema

{{ schema2md('./sources/schema/criteria/open-criteria-schema.yaml') }}

#### Open Examples

Short notation example of ```open```:

{{ includeScenario('./sources/examples/scenario/open-scenario-1.yaml') }}

Complex example:

{{ includeScenario('./sources/examples/scenario/open-scenario-2.yaml') }}

### Ensure
#### Ensure Step Schema

To verify the integrity of the page it may be reasonable to ensure the presence of a certain element. The action ```ensure``` verifies, whether the particular element is present on the page.

{{ schema2md('./sources/schema/steps/ensure-step-schema.yaml') }}

#### Ensure Criteria Schema

{{ schema2md('./sources/schema/criteria/ensure-criteria-schema.yaml') }}

#### Ensure Examples
The following simple scenario can be created using the shot-notation of ```ensure``` action:

1. Open a web page.
2. Verify the presence of a header with a certain class.

This would look like the following in WAML.

{{ includeScenario('./sources/examples/scenario/ensure-scenario-1.yaml') }}

Using the additional criteria not only the presence of the element can be ensured but also elements content and its appearance within a defined a time constraint.

{{ includeScenario('./sources/examples/scenario/ensure-scenario-2.yaml') }}

### Move
#### Move Step Schema

For hidden elements which appear only after the user has hovered a certain element the (mouse) ```move``` action can be used.  

{{ schema2md('./sources/schema/steps/move-step-schema.yaml') }}

#### Move Criteria Schema

{{ schema2md('./sources/schema/criteria/move-criteria-schema.yaml') }}

#### Move Example

The following example depicts the usage of the ```move``` action.

{{ includeScenario('./sources/examples/scenario/move-scenario-1.yaml') }}

Complex example:

{{ includeScenario('./sources/examples/scenario/move-scenario-2.yaml') }}


### Click
#### Click Step Schema

Every kind of clicks can be simulated with the ```click``` action.

{{ schema2md('./sources/schema/steps/click-step-schema.yaml') }}

#### Click Criteria Schema

{{ schema2md('./sources/schema/criteria/click-criteria-schema.yaml') }}

#### Click Examples

In the following short notation example click happens on an anchor element selected by CSS. 

{{ includeScenario('./sources/examples/scenario/click-scenario-1.yaml') }}

The ```text``` criteria may be used to verify the wording of the target.
 
{{ includeScenario('./sources/examples/scenario/click-scenario-2.yaml') }}


### Select
#### Select Step Schema

{{ schema2md('./sources/schema/steps/select-step-schema.yaml') }}

#### Select Criteria Schema

{{ schema2md('./sources/schema/criteria/select-criteria-schema.yaml') }}

#### Select Example

Short notation example of ```select```:

{{ includeScenario('./sources/examples/scenario/select-scenario-1.yaml') }}

Complex example:

{{ includeScenario('./sources/examples/scenario/select-scenario-2.yaml') }}


### Enter
#### Enter Step Schema

{{ schema2md('./sources/schema/steps/enter-step-schema.yaml') }}

#### Enter Criteria Schema

{{ schema2md('./sources/schema/criteria/enter-criteria-schema.yaml') }}

#### Enter Example

{{ includeScenario('./sources/examples/scenario/enter-scenario-1.yaml') }}


### Wait
#### Wait Step Schema

{{ schema2md('./sources/schema/steps/wait-step-schema.yaml') }}

#### Wait Criteria Schema

{{ schema2md('./sources/schema/criteria/wait-criteria-schema.yaml') }}

#### Wait Example

Short notation example of ```wait```:

{{ includeScenario('./sources/examples/scenario/wait-scenario-1.yaml') }}

#### Complex example
{{ includeScenario('./sources/examples/scenario/wait-scenario-2.yaml') }}


### Include
#### Include Step Schema

{{ schema2md('./sources/schema/steps/include-step-schema.yaml') }}

#### Include Criteria Schema

{{ schema2md('./sources/schema/criteria/include-criteria-schema.yaml') }}

#### Include Examples

Short notation example of ```include```:

{{ includeScenario('./sources/examples/scenario/include-scenario-1.yaml') }}

Complex example:

{{ includeScenario('./sources/examples/scenario/include-scenario-2.yaml') }}


### Store
#### Store Step Schema

{{ schema2md('./sources/schema/steps/store-step-schema.yaml') }}

#### Store Criteria Schema

{{ schema2md('./sources/schema/criteria/store-criteria-schema.yaml') }}

#### Store Examples

An example of simple usage of ```store```:

{{ includeScenario('./sources/examples/scenario/store-scenario-1.yaml') }}

Complex example:

{{ includeScenario('./sources/examples/scenario/store-scenario-2.yaml') }}


## Expressions
### Expression Schema

{{ schema2md('./sources/schema/expression-schema.yaml') }}

## Shared Criteria
### Parent Criteria Schema

{{ schema2md('./sources/schema/criteria/parent-criteria-schema.yaml') }}


## Management of Multiple Scenarios

A single WAML file may contain multiple scenarios. Therefore, the capability of YAML to store multiple documents by splitting them with ```---``` is used.




[YAML 1.2]: http://yaml.org/spec/1.2/spec.html
[RFC 2119]: https://www.ietf.org/rfc/rfc2119.txt

[JSON Schema]: http://json-schema.org/
[changelog]: CHANGELOG.md
[waml-json]: dist/waml.json
[waml-yaml]: dist/waml.yaml
[waml-schema.org]: http://waml-schema.org

