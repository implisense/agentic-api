# Implisense 🍰 Agentic API

Agentic API is a LLM-based assistant API capable of answering complex research questions, optimized for consistency and factual reliability. 
It is comprised of various task-specific agent subsystems, which are modularly combined to process requests of diverging complexity.

## Source

The full source code is available on [Codeberg](https://codeberg.org/implisense/agentic-api).

## Run 

### Deploy
Install all requirements and run directly from the CLI with:
```
python -m uvicorn main:app
```

Or use the provided Dockerfile and run as container with:
```
build -f Dockerfile -t agentic-api
docker run -it -p 8000:8000 agentic-api
```

### Test
Test if everything works after deployment via Curl:

```curl
curl -X POST -H 'Content-Type: application/json' http://localhost:8000/ -d '{"assistant": "research", "message": "Software company or donut company?", "context": "Implisense", "effort": "medium", "locale": "en", "cache": "True"}'
```

All agents support technical testing mode by setting the parameter `effort = low`.
Use `medium` for the standard configuration and `high` for experimental reasoning mode.
The automatic docs can be accessed via `http://localhost:8000/docs`.

### Env
The system requires paid API keys for both the LLMs from OpenAI and search functionality from Serper. 
They can be configured via environment variables or passed with each request. 
The full I/O model is specified in `/agentic_api/model/agent.py`.

Set your API key from [OpenAI](https://openai.com/api/) as `OPENAI_API_KEY`, your [Serper](https://serper.dev) key as `SERPER_API_KEY` and optionally specify a custom logging directory via `STATE_PATH`.

Various rate or access limits might apply for external services, especially for new accounts. 
External web search and LLM usage scales dynamically and is charged per request.

## Assistants
The following assistants are currently available:
```
contacts, classifier, meta, news, research, transform
```

Specify the required subsystem via the `assistant` parameter.
See the provided examples in `/samples/assistant.md` for additional guidance on functionality, prompting and context design.

## Locales
Agentic API currently supports these output languages:
```
"en": "English", "de": "German", "fr": "French", "es": "Spanish", "it": "Italian", 
"pt": "Portuguese", "ru": "Russian", "ja": "Japanese", "cn": "Chinese", "hi": "Hindi", 
"ar": "Arabic", "id": "Indonesian", "ko": "Korean", "tr": "Turkish", "fa": "Persian", 
"gr": "Greek", "pl": "Polish", "uk": "Ukrainian", "ro": "Romanian", "nl": "Dutch"
```

## Notes
We release our agentic research system primarily for scientific archival purposes, as it has been largely superseeded by various implementations of deep research systems, based on custom end-to-end models instead of using a mixture of prompt engineering and program logic.

However, for specific problem domains the additional layer of control and stability offered by this more granular approach might still be a preferable solution. 
Our system performed on par with comparable state-of-the-art agentic research systems until February 2025 in our internal benchmarks.

The API can be considered production-ready, with many months of extensive reliability testing and a mature I/O interface. 
Much could still be improved, of course.

All prompting is heavily optimized for GPT4-class models by OpenAI. 
Performance will likely degrade substantially if run on other model families or other model series by OpenAI.

We regard our snippet compression and lectoring systems as both novel and scalable solutions to their given problems.

## Todo
- Periodic model updates
- Full type safety for internal openai components 
- Proper asynchronous logging

## License
This software is licensed under the MIT License:
```
Copyright (c) 2025 Implisense

Permission is hereby granted, free of charge, to any person obtaining a copy of this software 
and associated documentation files (the "Software"), to deal in the Software without restriction, 
including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, 
and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, 
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial 
portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING 
BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND 
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, 
DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, 
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

## About
AgenticAPI is maintained and funded by [Implisense](https://implisense.com/).

![](https://cdn.prod.website-files.com/66018d2a187a2599c5d8cd67/66726d5c52eb30a892c8bcea_logo-word-f448b78ea7bf2a18913bfecb474cd26df397c564f1d0ad968f6299b849aa093f.svg)
