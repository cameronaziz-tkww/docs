# 🌳 Project File Tree

## Top Level File Tree
This outline of the file structure is not exhaustive
```cs
├── apps
│   ├── audit                                        // Tool to calculate Lighthouse scores
│   ├── marketplace-web                              // Main application
│   │   ├── __mocks__                                // Mocks that are mounted for EVERY test
│   │   ├── __stubs__                                // Stubs of various data needed for tests
│   │   ├── __test_support__                         // Mocks that are mounted for specific tests
│   │   ├── api                                      // API functions that call the Marketplace API
│   │   ├── client                                   // See `Client File Structure` below
│   │   ├── config                                   // XO Logger configurations
│   │   ├── deployment                               // Various deployment scripts
│   │   ├── docker                                   // Docker settings
│   │   ├── lib                                      // Modules that compiled on build; should NOT be extended
│   │   │   ├── marketplace-fe-shared                // Various modules
│   │   │   ├── pacarana                             // Analytics tracking methods and HOCs
│   │   │   ├── vendor-recommendation-module         // ogVRM - deperecation soon
│   │   │   └── xo-rfq-forms                         // RFQ forms, components and configurations
│   │   ├── scripts                                  // Docker test script
│   │   ├── server                                   // See `Server File Structure` below
│   │   ├── settings                                 // Settings HAVE to be placed in both files
│   │   │   ├── qa.js                                // Settings for local, pr instances and qa-beta
│   │   │   └── production.js                        // Settings for staging and production
│   │   ├── styleguide                               // Styleguide and engineering tips
│   │   ├── types                                    // Types, namespaces, and modules; not to be imported directly
│   │   └── utils                                    // Functions that are used throughout the application
│   └── storybook-app                                // Components rendered in isolation of the application
├── deployment                                       // Deployment configurations
├── packages                                         // Independent packages that are hosted on Gemfury
│   ├── ets-vendor-wrapper                           // Higher order component to wrap Vendor Card Component
│   ├── pagination                                   // Pagination Component
│   ├── pricing-calculator                           // Pricing Component for Vendor Storefronts
│   ├── states                                       // Tool to calculate Lighthouse scores
│   └── vendor-utils                                 // Vendor decorator and helpers
├── .codeclimate.yml                                 // Configuration for code climate
├── .dockerignore                                    // List of paths to be excluded from docker image
├── .eslintignore                                    // List of paths to for ESLint to ignore
├── .eslintrc                                        // ESLint rules
├── .gitignore                                       // List of paths for Git to ignore
├── .npmrc                                           // Private repository paths and authentication
├── docker-compose.yml                               // Docker configuration
├── Makefile                                         // Various scripts for running, testing and deployting
└── package.json                                     // Global package.json
```

## Client File Tree
This outline of the file structure is not exhaustive
```cs
├── components
│   ├── multi-category-vrm                           // MCVRM component
│   ├── shared                                       // Various shared components
│   └── storybook-app                                // Components rendered in isolation of the application
├── decorators                                       // Deployment configurations
│   ├── vendor                                       // Accepts raw vendor and returns vendor instantiation
│   └── vendorAnalytics                              // Accepts vendor instantiation and returns analytics object
├── googleAdManagerScripts                           // Google Ad Manager embedded HTML
├── helpers                                          // Helper functions
├── pages                                            // Each child folder containing a specific route
├── redux                                            // Redux reducers, action creators and thunks
├── routes                                           // Router configuration
├── utils                                            // Utility constants and functions;  should NOT be extended
├── .eslintrc                                        // ESLint rules specific for client
├── index.jsx                                        // Root React initializer
├── store.js                                         // Redux store creator
├── styles.scss                                      // Global SCSS
└── test.js                                          // Tests for index.jsx and store.js
```

## Server File Tree