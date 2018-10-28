![image](https://user-images.githubusercontent.com/2212651/47438511-e6b78880-d7aa-11e8-8cbb-74e4e859b589.png)

# Status Live

This repository is to store information for the project as part of #cryptolife hackathon to implement livestreaming functionality in Status App using Livepeer's open-source video infrastructure.

## Context

Status is holding a hackathon from 26-29 October 2018. The objective is to develop apps and dApps to allow more people to live a _cryptolife_: a life based entirely on cryptocurrencies.

[Status](https://status.im/) has a _Mobile Ethereum Operating System_ app for Android, which includes wallet functionality.

[Livepeer](https://livepeer.org/) is an open-source video infrastructure, with services for livestreaming.

## Objective

The objective of this project is to build minimal viable livestreaming functionality in Status App for Android, using Livepeer video infrastructure.

## Result

The team was able to add a "go live" button in the "New" page in status (the "+" sign on the top right corner). The button should bring up a camera screen that enables a broadcast, but unfortunately we couldn't test it due to the lack of camera access in the iOS simulator. (We couldn't get Android to compile). 

We used an existing [react-native RTMP library](https://github.com/NodeMedia/react-native-nodemediaclient) to do the implementation, and the code lives in the `livepeer` branch of @gomesalexandre's [repo](https://github.com/gomesalexandre/status-react).

Here is the instruction to run the repo:
1. Clone the repo `git clone https://github.com/gomesalexandre/status-react.git`
2. Check out the `livepeer` branch by `cd status-react && git checkout livepeer && cd ..`
3. Install the `nodemediaclient` react-native module: `yarn add react-native-nodemediaclient`
4. Link the module: `react-native link`
5. Install the pod: `cd ios && pod install && cd ..`
6. Run the status app as you would: `react-native run-ios`

The next step of the project is to test the camera on a real device, and to create a video ingest node discovery service so a number of Livepeer ingest nodes can be discovered, and the rtmp connection information can be fill in to the [NodeCameraView](https://github.com/gomesalexandre/status-react/blob/6ec7415f6fc4cf2e5e9fc3cf5997c2d744e204e5/src/status_im/ui/screens/go_live/views.cljs#L34)

The video ingest node discovery service can start as a simple service that has knowledge about Status-deployed Livepeer nodes. The service can find a ingest node that doesn't currently have a stream running, and return the RTMP endpoint to the Status client so it can send the broadcast video to that ingest node.

@ericxtang is happy to help advise the creation of such service.
