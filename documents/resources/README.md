# 💎 Resources
We use various resources to track metrics and monitor bugs
## Github
Github is the service we use to host our Git repositories
### Authentication
Login is through [XO Okta](https://xo.okta.com/). A request [Help Desk](mailto:helpdesk@theknotww.com) to give access to the following organizations will be required:
- tkww
- xogroup
When submitting the request, Help Desk will require for you to provide a Github login (handle) that is not a personal login
## Jenkins

Jenkins is the service we use for our CI/CD build processes
### Authentication
Login is through SSO. A request [Help Desk](mailto:helpdesk@theknotww.com) to give access Jenkins will be required:
When submitting the request, Help Desk will require for you to provide a Github login (handle) that is not a personal login, as they are attached
## Cisco VPN
Cisco VPN is uses to access certain resources from outside of the corporate network. The client can be downloaded from [here](https://www.cisco.com/c/en/us/support/security/anyconnect-secure-mobility-client-v4-x/model.html#~tab-downloads)

## Honeybadger
Honeybadger is used to track bugs, triggered both server side and client side
### Authentication
Login is through [XO Okta](https://xo.okta.com/). A request [Help Desk](mailto:helpdesk@theknotww.com) to give access to the following applications will be required:
- Marketplace
### Resources
| Application | Project                                                                       |
| ----------- | ----------------------------------------------------------------------------- |
| New Coke    | [hapi-marketplace-web-prod](https://app.honeybadger.io/projects/58283/faults) |
| Classic     | [prod-marketplace](https://app.honeybadger.io/projects/35685/faults)          |
| Inbox       | [inbox-production](https://app.honeybadger.io/projects/46668/faults)          |

## New Relic
New Relic is used to monitor live performance
### Authentication
Login is through [XO Okta](https://xo.okta.com/). A request [Help Desk](mailto:helpdesk@theknotww.com) to give access to the following accounts will be required:
- XO-WedMarket
- XO-LocalVendors
### Resources
| Application          | Account         | Service                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------------------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Frontend Application | XO-WedMarket    | [Hapi Marketplace Web](https://one.newrelic.com/launcher/nr1-core.explorer?platform[tvMode]=false&platform[accountId]=370406&platform[filters]=Iihkb21haW4gPSAnQVBNJyBBTkQgdHlwZSA9ICdBUFBMSUNBVElPTicpIg==&platform[timeRange][duration]=1800000&platform[$isFallbackTimeRange]=true&pane=eyJuZXJkbGV0SWQiOiJhcG0tbmVyZGxldHMub3ZlcnZpZXciLCJlbnRpdHlHdWlkIjoiTXpjd05EQTFmRUZRVFh4QlVGQk1TVU5CVkVsUFRud3hOekk0T1RneE5ETSIsImlzT3ZlcnZpZXciOnRydWV9)                                                                          |
| Main API             | XO-LocalVendors | [Locals__service-marketplace-api__PRODUCTION](https://one.newrelic.com/launcher/nr1-core.explorer?platform[tvMode]=false&platform[accountId]=370406&platform[filters]=Iihkb21haW4gPSAnQVBNJyBBTkQgdHlwZSA9ICdBUFBMSUNBVElPTicpIg==&platform[timeRange][duration]=1800000&platform[$isFallbackTimeRange]=true&launcher=eyJzZWxlY3RlZEluc3RhbmNlIjpudWxsLCJ0cmFuc2FjdGlvblR5cGUiOm51bGx9&pane=eyJuZXJkbGV0SWQiOiJhcG0tbmVyZGxldHMub3ZlcnZpZXciLCJlbnRpdHlHdWlkIjoiTXpjd05EQTJmRUZRVFh4QlVGQk1TVU5CVkVsUFRud3lPVFUyT1RjeU5RIn0=) |
| Conversations API    | XO-LocalVendors | [Locals__service-conversation-theknot-api__PRODUCTION](https://one.newrelic.com/launcher/nr1-core.explorer?platform[tvMode]=false&platform[accountId]=370406&platform[filters]=Iihkb21haW4gPSAnQVBNJyBBTkQgdHlwZSA9ICdBUFBMSUNBVElPTicpIg==&platform[timeRange][duration]=1800000&platform[$isFallbackTimeRange]=true&pane=eyJuZXJkbGV0SWQiOiJhcG0tbmVyZGxldHMub3ZlcnZpZXciLCJlbnRpdHlHdWlkIjoiTXpjd05EQTJmRUZRVFh4QlVGQk1TVU5CVkVsUFRud3hOVGsxTURjek9RIiwiaXNPdmVydmlldyI6dHJ1ZX0=)                                          |

## SpeedCurve
SpeedCurve is used to monitor code performance
### Authentication
Login is through SSO. Team manager can give access
### Resources

| Metrics        | Dashboard                                                                                                                                               |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SEO            | [Marketplace FE SEO](https://speedcurve.com/xo/marketplace/favorite/?cs=lg&d=30&db=7353&dc=2&de=1&df=%7B%7D&ds=1)                                       |
| Vitals         | [State and Category Pages](https://speedcurve.com/xo/marketplace/vitals-syn/?b=apple-iphone-6-plus&cs=lg&d=30&de=1&ds=1&label=Category%20Page&s=214757) |
| DOM Load Times | [Status](https://speedcurve.com/xo/marketplace/status/)                                                                                                 |

## NodePing
NodePing is used to ensure pages are being returned from the server. After login, performing a search for the target will return current status
### Authentication
Login is through [XO Okta](https://xo.okta.com/). A request [Help Desk](mailto:helpdesk@theknotww.com) to give access will be required
### Resources

| Page       | Target                                                                                             |
| ---------- | -------------------------------------------------------------------------------------------------- |
| Home       | Market - tk/marketplace               \| Home -> marketplace.theknot.com (LVAWS) Team: Marketplace |
| Storefront | Market - tk/marketplace \| Storefront                                                              |
| Search     | Market - tk/marketplace               \| Search                                                    |

## Code Climate
Code Climate is used to monitor code quality and test coverage. Metrics for a given branch are available through Github after a pull request has been created
### Authentication
Login is through Github SSO. Team manager can give access
### Resources
| Repository    | Dashboard                                                      |
| ------------- | -------------------------------------------------------------- |
| TKMarketplace | [Link](https://codeclimate.com/repos/5e1e4e30610531018d009272) |
