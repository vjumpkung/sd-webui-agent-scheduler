# Agent Scheduler

This version is porting to WebUI Forge by updating extension into pydantic 2 and gradio 4

## Known Issue

- Enqueue button not working properly in first time when launch WebUI Forge but you can refresh to make it working (idk why?)

- Generation Info Gone

- This Extension is only working in WebUI Forge something maybe not tested yet if you found issue please report in issue tab.

## Description (TH)

- Extension นี้เป็นการแปลงให้ WebUI Forge ใช้งานได้เท่านั้น อาจมีบางอย่างที่ยังไม่ได้เทส หากมีปัญหาโปรดแจ้งใน issue

## Table of Content

- [Agent Scheduler](#agent-scheduler)
  - [Known Issue](#known-issue)
  - [Description (TH)](#description-th)
  - [Table of Content](#table-of-content)
  - [Compatibility](#compatibility)
  - [Installation](#installation)
    - [Using the built-in extension list](#using-the-built-in-extension-list)
    - [Manual clone](#manual-clone)
  - [Basic Features](#basic-features)
  - [Hidden Features:](#hidden-features)
      - [Queue all checkpoints at the same time](#queue-all-checkpoints-at-the-same-time)
      - [Queue with a subset of checkpoints](#queue-with-a-subset-of-checkpoints)
      - [Edit queued task](#edit-queued-task)
  - [Extension Settings](#extension-settings)
  - [API Access](#api-access)
      - [Queue Task](#queue-task)
      - [Download Results](#download-results)
      - [API Callback](#api-callback)
  - [Troubleshooting](#troubleshooting)
  - [Contributing](#contributing)
  - [License](#license)
  - [Disclaimer](#disclaimer)
  - [CRAFTED BY THE PEOPLE BUILDING **SIPHER//AGI**, **PROTOGAIA**, **ATHERLABS** \& **SIPHER ODYSSEY**](#crafted-by-the-people-building-sipheragi-protogaia-atherlabs--sipher-odyssey)
    - [About ProtoGAIA](#about-protogaia)
    - [Current protoGAIA Features](#current-protogaia-features)
    - [Target Audience](#target-audience)
  - [🎉 Stay Tuned for Updates](#-stay-tuned-for-updates)

---

## Compatibility

This version of AgentScheduler is compatible with latest versions of:

- Forge : [commit c055f2d](https://github.com/lllyasviel/stable-diffusion-webui-forge/tree/c055f2d43b07cbfd87ac3da4899a6d7ee52ebab9)

> A1111 and Vlad not working anymore.

## Installation

### Using the built-in extension list

1. Open the Extensions tab
2. Open the "Install From URL" sub-tab
3. Paste the repo url: https://github.com/vjumpkung/sd-webui-agent-scheduler.git
4. Click "Install"

![Install](docs/images/install.png)

### Manual clone

```bash
git clone "https://github.com/vjumpkung/sd-webui-agent-scheduler.git" extensions/agent-scheduler
```

(The second argument specifies the name of the folder, you can choose whatever you like).

## Basic Features

![Extension Walkthrough 1](https://github.com/ArtVentureX/sd-webui-agent-scheduler/assets/133728487/a5a039a7-d98b-4186-9131-6775f0812c39)

1️⃣ Input your usual Prompts & Settings. **Enqueue** to send your current prompts, settings, controlnets to **AgentScheduler**.

![Extension Walkthrough 2](https://github.com/ArtVentureX/sd-webui-agent-scheduler/assets/133728487/734176b4-7ee3-40e5-bb92-35608fabfc4b)

2️⃣ **AgentScheduler** Extension Tab.

3️⃣ See all queued tasks, current image being generated and tasks' associated information. **Drag and drop** the handle in the begining of each row to reaggrange the generation order.

4️⃣ **Pause** to stop queue auto generation. **Resume** to start.

5️⃣ Press ▶️ to prioritize selected task, or to start a single task when queue is paused. **Delete** tasks that you no longer want.

![ Extension Walkthrough 3](https://github.com/ArtVentureX/sd-webui-agent-scheduler/assets/133728487/23109761-2633-4b24-bbb3-091628367047)

6️⃣ Show queue history.

7️⃣ **Filter** task status or search by text.

8️⃣ **Bookmark** task to easier filtering.

9️⃣ Double click the task id to **rename** and quickly update basic parameters. Click ↩️ to **Requeue** old task.

🔟 Click on each task to **view** the generation results.

https://github.com/ArtVentureX/sd-webui-agent-scheduler/assets/133728487/50c74922-b85f-493c-9be8-b8e78f0cd061

## Hidden Features:

#### Queue all checkpoints at the same time

Right click the `Enqueue` button and select `Queue with all checkpoints` to quickly queue the current setting with all available checkpoints.

![image](https://github.com/ArtVentureX/sd-webui-agent-scheduler/assets/133728487/c75276e8-6d0c-4f72-91db-817f38a3fea6)

#### Queue with a subset of checkpoints

![image](https://github.com/ArtVentureX/sd-webui-agent-scheduler/assets/133728487/b776d09d-c789-47f1-8884-975848bb766d)

![image](https://github.com/ArtVentureX/sd-webui-agent-scheduler/assets/133728487/bdb2b41a-5ae8-41c1-bece-7dbff67e38b7)

With the custom checkpoint select enabled (see [Extension Settings](#extension-settings) section below), you can select a folder (or subfolder) to queue task with all checkpoints inside. Eg: Select `anime` will queue `anime\AOM3A1B_oragemixs`, `anime\counterfeit\Counterfeit-V2.5_fp16` and `anime\counterfeit\Counterfeit-V2.5_pruned`.

#### Edit queued task

Double click a queued task to edit. You can name a task by changing `task_id` or update some basic parameters: `prompt`, `negative prompt`, `sampler`, `checkpoint`, `steps`, `cfg scale`.

![image](https://github.com/ArtVentureX/sd-webui-agent-scheduler/assets/133728487/57535174-2f66-4ee7-8f3c-9f1dd3882eff)

## Extension Settings

Go to `Settings > Agent Scheduler` to access extension settings.

![Settings](https://github.com/ArtVentureX/sd-webui-agent-scheduler/assets/133728487/b0377ccd-f9bf-486e-8393-c06fe26aa117)

**Disable Queue Auto-Processing**: Check this option to disable queue auto-processing on start-up. You can also temporarily pause or resume the queue from the Extension tab.

**Queue Button Placement**: Change the placement of the queue button on the UI.

**Hide the Checkpoint Dropdown**: The Extension provides a custom checkpoint dropdown.

![Custom Checkpoint](https://github.com/ArtVentureX/sd-webui-agent-scheduler/assets/133728487/d110d314-a208-4eec-bb54-9f8c73cb450b)

By default, queued tasks use the currently loaded checkpoint. However, changing the system checkpoint requires some time to load the checkpoint into memory, and you also cannot change the checkpoint during image generation. You can use this dropdown to quickly queue a task with a custom checkpoint.

**Auto Delete Queue History**: Select a timeframe to keep your queue history. Tasks that are older than the configured value will be automatically deleted. Please note that bookmarked tasks will not be deleted.

## API Access

All the functionality of this extension can be accessed through HTTP APIs. You can access the API documentation via `http://127.0.0.1:7860/docs`. Remember to include `--api` in your startup arguments.

![API docs](https://github.com/ArtVentureX/sd-webui-agent-scheduler/assets/133728487/012ab2cc-b41f-4c68-8fa5-7ab4e49aa91d)

#### Queue Task

The two apis `/agent-scheduler/v1/queue/txt2img` and `/agent-scheduler/v1/queue/img2img` support all the parameters of the original webui apis. These apis response the task id, which can be used to perform updates later.

```json
{
  "task_id": "string"
}
```

#### Download Results

Use api `/agent-scheduler/v1/results/{id}` to get the generated images. The api supports two response format:

- json with base64 encoded

```json
{
  "success": true,
  "data": [
    {
      "image": "data:image/png;base64,iVBORw0KGgoAAAAN...",
      "infotext": "1girl\nNegative prompt: EasyNegative, badhandv4..."
    },
    {
      "image": "data:image/png;base64,iVBORw0KGgoAAAAN...",
      "infotext": "1girl\nNegative prompt: EasyNegative, badhandv4..."
    }
  ]
}
```

- zip file with querystring `zip=true`

#### API Callback

Queue task with param `callback_url` to register an API callback. Eg:

```json
{
  "prompt": "1girl",
  "negative_prompt": "easynegative",
  "callback_url": "http://somehost:port/task_completed"
}
```

The callback endpoint must support `POST` method with body in `multipart/form-data` encoding. Body format:

```json
{
  "task_id": "abc123",
  "status": "done",
  "files": [list of image files],
}
```

Example code of the endpoint handle with `FastApi`:

```python
from fastapi import FastAPI, UploadFile, File, Form

@app.post("/task_completed")
async def handle_task_completed(
    task_id: Annotated[str, Form()],
    status: Annotated[str, Form()],
    files: Optional[List[UploadFile]] = File(None),
):
    print(f"Received {len(files)} files for task {task_id} with status {status}")
    for file in files:
        print(f"* {file.filename} {file.content_type} {file.size}")
        # ... do something with the file contents ...

# Received 1 files for task 3cf8b150-f260-4489-b6e8-d86ed8a564ca with status done
# * 00008-3322209480.png image/png 416400
```

## Troubleshooting

Make sure that you are running the latest version of the extension and an updated version of the WebUI.

- To update the extension, go to `Extension` tab and click `Check for Updates`, then click `Apply and restart UI`.
- To update the WebUI it self, you run the command `git pull origin master` in the same folder as webui.bat (or webui.sh).

Steps to try to find the cause of issues:

- Check the for errors in the WebUI output console.
- Press F12 in the browser then go to the console tab and reload the page, find any error message here.

Common errors:

**AttributeError: module 'modules.script_callbacks' has no attribute 'on_before_reload'**

If you see this error message in the output console, try update the WebUI to the latest version.

**Update**: The extension is updated to print this warning message instead: **YOUR SD WEBUI IS OUTDATED AND AGENT SCHEDULER WILL NOT WORKING PROPERLY.** You can still able to use the extension but it will not working correctly after a reload.

~~**ReferenceError: submit_enqueue is not defined**~~

~~If you click the `Enqueue` button and nothing happen, and you find above error message in the browser F12 console, follow the steps in [this comment](https://github.com/ArtVentureX/sd-webui-agent-scheduler/issues/4#issuecomment-1575986274).~~

Update: This issue is now fixed.

**TypeError: issubclass() arg 1 must be a class**
Please update the extension, there's a chance it's already fixed.

**TypeError: Object of type X is not JSON serializable**
Please update the extension, it should be fixed already. If not, please fire an issue report with the list of installed extensions.

For other errors, feel free to fire a new [Github issue](https://github.com/ArtVentureX/sd-webui-agent-scheduler/issues/new/choose).


## Contributing

We welcome contributions to the Agent Scheduler Extension project! Please feel free to submit issues, bug reports, and feature requests through the GitHub repository.

Please give us a ⭐ if you find this extension helpful!

## License

This project is licensed under the Apache License 2.0.

## Disclaimer

The author(s) of this project are not responsible for any damages or legal issues arising from the use of this software. Users are solely responsible for ensuring that they comply with any applicable laws and regulations when using this software and assume all risks associated with its use. The author(s) are not responsible for any copyright violations or legal issues arising from the use of input or output content.

---

## CRAFTED BY THE PEOPLE BUILDING [**SIPHER//AGI**](https://sipheragi.com), [**PROTOGAIA**](https://protogaia.com), [**ATHERLABS**](https://atherlabs.com/) & [**SIPHER ODYSSEY**](http://playsipher.com/)

### About ProtoGAIA

ProtoGAIA offers powerful collaboration features for Generative AI Image workflows. It is designed to help designers and creative professionals of all levels collaborate more efficiently, unleash their creativity, and have full transparency and tracking over the creation process.

### Current protoGAIA Features

Like any open project that seeks to bring the powerful of Generative AI to the masses, ProtoGAIA offers the following key features:

✅ Seamless Access: available on desktop and mobile

✅ Powerful Macro Abilities that allowing the chaining of tasks, which is then packaged as Macro Command ready for AI Agent Automation

✅ Multiplayer & Collaborative UX. Strong collaboration features, such as real-time commenting and feedback, version control, and image/file/project sharing

✅ Rooms Chat for lively discussion between users and running Generative AI workflows right in the chat

✅ Custom Models Management including Lora, Diffusion Models, Controlnet Models and more

✅ Powerful semantic search capabilities

✅ Powerful AI driven chat box that can trigger quick Generative AI tasks and workflows

✅ Building on shoulders of Giants, leveraging A1111/Vladnmandic and other pioneers, provide collaboration process from Idea to Final Results in 1 platform

✅ Automation tooling for certain repeated tasks

✅ Secure and transparent, leveraging hasing and metadata to track the origin and history of models, loras, images to allow for tracability and ease of collaboration

✅ Personalize UIUX for both beginner and experienced users to quickly remix existing SD images by editing prompts and negative prompts, selecting new training models and output quality as desired

✅ Provenance Tracking for all models, loras, images to allow for tracability and ease of collaboration

✅ Custom UIUX for both beginner and experienced users to quickly remix existing SD images by editing prompts and negative prompts, selecting new training models and output quality as desired

✅ Articles and Tutorials for learning Generative AI

✅ Voting System for best generative AI images, models, recipes, macros etc

✅ Open sharing of generative AI images, models, recipes, macros etc via the Global Explore tab

### Target Audience

ProtoGAIA is designed for the following target audiences:

- Creators
- Small Design Teams or Freelancers
- Design Agencies & Game Studios
- AI Agents

## 🎉 Stay Tuned for Updates

We hope you find this extension to be useful. We will be adding new features and improvements over time as we enhance this extension to support our creative workflows.

To stay up-to-date with the latest news and updates, be sure to follow us on GitHub and Twitter. We welcome your feedback and suggestions, and are excited to hear how AgentScheduler can help you streamline your workflow and unleash your creativity!
