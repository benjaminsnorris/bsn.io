---
title:          Adding automation to open-source projects
date:           2016-09-10 13:00:00
summary:        Improving projects and increasing self-guilt with Travis and Codecov
categories:     reference testing
---

1. Set up [Travis](https://travis-ci.org/) to start building
1. Add `.travis.yml` to project (include sample)
1. Make sure to build either project or workspace, as needed
1. Set up [Codecov](https://codecov.io/) to collect coverage
1. Add [Slather](https://github.com/SlatherOrg/slather) to limit to Sources (include sample)
1. Test locally
  - `xcodebuild -workspace TextMagic.xcworkspace -scheme TextMagic -sdk iphonesimulator9.3 -destination="OS=9.3,name=iPhone 6S Plus" -configuration Debug GCC_INSTRUMENT_PROGRAM_FLOW_ARCS=YES GCC_GENERATE_TEST_COVERAGE_FILES=YES ONLY_ACTIVE_ARCH=YES test | xcpretty -c`
  - `slather coverage -s --scheme TextMagic --workspace TextMagic.xcworkspace/ TextMagic.xcodeproj/`

`ONLY_ACTIVE_ARCH=YES` <- important
