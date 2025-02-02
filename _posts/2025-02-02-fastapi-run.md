---
title: Run FastAPI Server
date: 2025-02-02 01:01:01 +0700
categories: [fastapi]
tags: [fastapi]     # TAG names should always be lowercase
---

## Method-1: Run FastAPI by calling uvicorn.run(...)
```python
# main.py

import uvicorn
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def read_root():
    return {"Hello": "World"}


if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

Normally, you'll start the server by running the following command
```powershell
python main.py
```