# serving-stack

The one system this course builds. Your team creates this repository once from
the template, and every lab from week 2 to graduation is a change to it. There
is no week where you start again.

## What is here

```
app/        empty. Your service goes here, starting week 2 day 2
docs/       the API contract the Agentic AI cohort integrates against
scripts/    verify-env.sh, which checks your machine against what the labs need
PINS.md     every version this course depends on
setup.md    how to work in this repository
```

That is the whole repository, and the shortness of that list is the point. You
are not given a finished system to read. You build one, a day at a time, and by
week 6 another cohort's agents are calling it.

## What you add, and when

| Week | Day | What you add |
|---|---|---|
| 2 | Mon | `app/` behind an OpenAI-compatible `/v1` on CPU |
| 2 | Tue | `Dockerfile`, and your image on Docker Hub |
| 2 | Wed | `Dockerfile.gpu`, the same code on a GPU |
| 2 | Thu | `compose.yaml`, the stack described rather than run by hand |
| 3 | Thu | `bench/`, the harness that measures all of it |

Each one is a lab, and each one starts from files that day hands you. Lab
instructions, decks and quizzes are on the course Drive, one folder per week.
This repository is your code.

## Start here

```bash
./scripts/verify-env.sh     # checks your machine, writes verify-env-report.json
```

Then read `setup.md`. It is short, and it covers the two things that go wrong:
committing a key, and committing a model.

## W2D2 wrap a model  

## Predict

Before implementing the routes, my predictions were:

* After sending one chat request with a **10-word user message** and asking for **32 tokens back**, I expected `usage.prompt_tokens` to be about **30 tokens** and `usage.completion_tokens` to be about **32 tokens**.

* Which of the three routes will pass its test first, with the least code?
  **`GET /health`**

* Will an unmodified `openai` Python client work against the server with only a `base_url` change?

   **Yes** ,  the server follows the OpenAI-compatible API contract, so the standard OpenAI Python client can communicate with it by changing the `base_url` to the local service. The request and response structures remain compatible with what the client expects.

  Step 1:
  
  <img width="648" height="150" alt="image" src="https://github.com/user-attachments/assets/e8f77601-6697-4fd4-be00-72520cf03982" />

  Step 2:

  <img width="770" height="129" alt="image" src="https://github.com/user-attachments/assets/d7560bc8-8716-4d34-bc53-d50bb3a0f5cf" />

  Step 3:

  <img width="766" height="181" alt="WhatsApp Image 2026-08-24 at 4 33 33 PM" src="https://github.com/user-attachments/assets/f2602237-f8da-4d87-acbe-93be36fd34ec" />

  Step 4:

  <img width="441" height="65" alt="{EC6D5548-C777-4817-BA09-4785759DB510}" src="https://github.com/user-attachments/assets/285fafb9-7189-498a-a381-d672bcc4803f" />


  Step 5:

  <img width="433" height="106" alt="{04BAE2B5-2B05-4981-A20E-4303313AF763}" src="https://github.com/user-attachments/assets/6b42aad6-2451-4eb6-aaef-4626d038b2c0" />


  Verification:

  <img width="883" height="213" alt="WhatsApp Image 2026-08-24 at 4 44 01 PM" src="https://github.com/user-attachments/assets/e6e43a2c-6e24-40b8-ab85-4f8e96af8cb5" />


  

## W2D3 Containerisation 

### Actual Image Sizes

After building and measuring both images:

| Stage | Actual Image Size |
|---|---:|
| Naive build (full base, cached pip) | **9.69 GB** |
| Slim build (slim base, CPU PyTorch, no pip cache) | **3.43 GB** |

The optimized image was **6.26 GB smaller** than the naive image, a reduction of approximately **65%**.

Verification step:
<img width="999" height="190" alt="image" src="https://github.com/user-attachments/assets/bd1e3651-ceb5-4371-bad8-330f7d45bfa0" />


## W2D4 GPU image

### Predict
Before building or running the GPU image, I predict:

/health status on my GPU-less laptop: **ok — the container will use the CPU fallback.**
128-token generation on laptop CPU: **about 5 tokens/sec.**
128-token generation on Colab T4 GPU: **about 25 tokens/sec.**
T4-to-CPU speed ratio: **roughly 5× faster.**


Verification step:
<img width="412" height="75" alt="{9DDDE35A-2480-4D92-AD3D-0EDF854652CD}" src="https://github.com/user-attachments/assets/b84807c5-e0ed-4799-8591-2e46796b4faf" />

## W2D5 compose

Verification step:
<img width="769" height="152" alt="image" src="https://github.com/user-attachments/assets/1dee0d10-05c4-42e2-9cda-3fd2d3af1a72" />


