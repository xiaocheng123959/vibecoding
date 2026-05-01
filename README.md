# Latte Art Drop

An MVP web app for generating AI latte-art images and dispatching them to a school coffee machine queue.

## Tech Stack

- Next.js (App Router + React Server Components)
- Tailwind CSS
- Framer Motion
- Vercel deployment

## Local Setup

1. Install dependencies:

```bash
npm install
```

2. Configure environment variables in `.env.local`:

```bash
COZE_API_KEY=your_real_key_here
```

Optional values:

```bash
COZE_STREAM_RUN_URL=https://hbyjqmt526.coze.site/stream_run
COZE_IMAGE_API_URL=https://api.coze.cn/v1/workflow/stream_run
COZE_PROJECT_ID=your_project_id
COZE_SESSION_ID=optional_fixed_session_id
SCHOOL_COFFEE_MACHINE_ENDPOINT=https://coffee-campus.example.com/api/print
SCHOOL_COFFEE_MACHINE_TOKEN=your_machine_token
```

3. Start development server:

```bash
npm run dev
```

4. Open http://localhost:3000

## API Routes

- `POST /api/generate`
	- Input: `{ "prompt": "..." }`
	- Output: generated image URL
	- Uses Coze `stream_run` with SSE parsing when `COZE_API_KEY` + `COZE_PROJECT_ID` are configured.
	- If Coze is not configured or fails, route returns a fallback image provider URL.

- `POST /api/dispatch`
	- Input: `{ "machineId": "school-cafe-01", "imageUrl": "..." }`
	- Sends to `SCHOOL_COFFEE_MACHINE_ENDPOINT` when configured
	- Otherwise returns mock queued status for local development

## Security

- `.env.local` is ignored by Git through `.gitignore` (`.env*` pattern).
- Never commit your real `COZE_API_KEY`.

## Deploy to Vercel

1. Push project to GitHub.
2. Import repository in Vercel.
3. Add environment variables in Vercel Project Settings:
	 - `COZE_API_KEY`
	 - Optional: `COZE_IMAGE_API_URL`, `SCHOOL_COFFEE_MACHINE_ENDPOINT`, `SCHOOL_COFFEE_MACHINE_TOKEN`
4. Deploy.
