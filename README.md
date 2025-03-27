# Example app: weather-service

This app uses pre-stored city-wise weather information in database to
be used as a tool to answer weather related questions.

## Usage

You need a Unix-compatible (macOS, Linux or Windows [WSL](https://learn.microsoft.com/en-us/windows/wsl/install))
system to run this app. Open a terminal and execute the steps below:

To run this app you need to define these env vars:

```shell
export OPENAI_API_KEY="FIXME" # your OpenAI API key
```

You may run this app without making a local copy first (i.e. clone the repo)
using Docker as follows:

```shell
docker run --rm \
  -p "0.0.0.0:8080:8080" \
  -v $PWD:/agentlang \
  -e OPENAI_API_KEY="$OPENAI_API_KEY" \
  -it agentlang/agentlang.cli:latest \
  agent clonerun https://github.com/agentlang-hub/weather-service.git
```

### Running a local copy of the app

If you have cloned the app and made a local copy on your computer,
you may run it using Docker as follows:

```shell
docker run --rm \
  -p "0.0.0.0:8080:8080" \
  -v $PWD:/agentlang \
  -e OPENAI_API_KEY="$OPENAI_API_KEY" \
  -it agentlang/agentlang.cli:latest \
  agent run
```

Alternatively, instead of Docker you may use the locally installed
[Agentlang CLI](https://github.com/agentlang-ai/agentlang.cli):

```shell
agent run
```

### Getting the app to provide verified answers

Make a request to ask a question as follows:

```shell
curl -X POST \
  localhost:8080/api/Weather.Service.Core/WeatherPlannerAgent \
  -H 'Content-type: application/json' \
  -d '{"Weather.Service.Core/WeatherPlannerAgent": {"UserInstruction": "What is the weather for Boston today?"}}'
```

It should respond with a JSON response body, example below:

```json
{
  "result": {
    "Temperature": 70.4,
    "Id": "47ce8543-1f73-4121-810b-30f3908f1d8d",
    "City": "Boston",
    "Date": "2025-03-27T18:19:23.213767208",
    "__path__": ":Weather.Service.Core/Weather,47ce8543-1f73-4121-810b-30f3908f1d8d",
    "Description": null,
    "__parent__": null
  },
  "status": "ok",
  "type": "Weather.Service.Core/Weather"
}
```

## License

Copyright 2024-2025 Fractl Inc.

Licensed under the Apache License, Version 2.0:
http://www.apache.org/licenses/LICENSE-2.0

