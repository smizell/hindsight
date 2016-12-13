# Hindsight

Hindsight is a proof of concept for a format for description applications. This takes a workflow- and interaction-centered approach to application design rather than starting with implementation details around protocols and schemas.

## Properties

- `interactions`

    Interactions include scenarios in the API, and capture snapshots of what the state of resources look like.

    - Properties
        - *interaction-name*
            - `title` - Title of the interaction
            - `description` - Description of the interaction
            - `scenarios`
                - *scenario-name*
                    - `when` - Context of the scenario
                        - *context* - User-defined context for the given scenario
                    - `then` - Expectations for the given scenario as defined by the `when`
                        - `links` (array[string]) - Expected links in the scenario
                        - `actions` (array[string]) - Expected actions in the scenario
                        - `status` - Expected status of the response

- `workflows`

    Workflows are paths through the API that a user may take to accomplish some specific work.

    - Properties
        - *workflow-name*
            - `title` - Title of the workflow
            - `description` - Description of the workflow
            - `steps` (array)
                - (enum)
                    - (object)
                        - `enter` - Scenario to use for entrance into the API
                            - `name` - Name of the interaction
                            - `scenario` - Scenario of the interaction
                    - (object)
                        - `follow`
                        - `interaction`
                            - `name` - Name of the interaction
                            - `scenario` - Scenario of the interaction
                    - (object)
                        - `submit` - Name of the action to invoke
                        - `data` - Data to send with the action
                        - `interaction`
                            - `name` - Name of the interaction
                            - `scenario` - Scenario of the interaction
- `definitions`

    Definitions define various semantics for the API.

    - Properties
        - `properties`
            - *property-name*
                - `title` - Title of the property
                - `description` - Description of the property
        - `links`
            - *link-name*
                - `title` - Title of the link
                - `description` - Description of the link
                - `specHref` - URL of a specification for the link
        - `actions`
            - *action-name*
                - `title` - Title of the action
                - `description` - Description of the action
  
- `protocols`

    Protocols is the section where we map the application logic and semantics to existing application protocols like HTTP.

    - Properties
        - `http`
            - *url-name*
                - `title` - Title of the URL
                - `description`
                - `urlTemplate` - URL Template for the given URL
                - `methods`
                    - *http-method* - HTTP method and the name of the interaction to use for it

## Resources

This is based on the blog post on [Thinking Through Hypermedia Design](http://smizell.com/weblog/2016/hypermedia-design).

This also borrows from existing ideas:

- [ALPS](http://alps.io)
- [Resource Blueprint](https://github.com/resource-blueprint/resource-blueprint)
- [Gherkin](https://github.com/cucumber/cucumber/wiki/Gherkin)
