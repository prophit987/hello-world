# hello-world
intro project lesson one
dontia moore-owner-edited-name-describing changes
# iOS CircleCI 2.0 configuration file
#
# Check https://circleci.com/docs/2.0/ios-migrating-from-1-2/ for more details
#
version: 2
jobs:
  build:

    # Specify the Xcode version to use
    macos:
      xcode: "8.3.3"

    steps:
      - checkout

      # Install CocoaPods
      - run:
          name: Install CocoaPods
          command: pod install

      # Build the app and run tests
      - run:
          name: Build and run tests
          command: fastlane scan
          environment:
            SCAN_DEVICE: iPhone 6
            SCAN_SCHEME: WebTests

      # Collect XML test results data to show in the UI,
      # and save the same XML files under test-results folder
      # in the Artifacts tab
      - store_test_results:
          path: test_output/report.xml
      - store_artifacts:
          path: /tmp/test-results
          destination: scan-test-results
      - store_artifacts:
          path: ~/Library/Logs/scan
          destination: scan-logs
