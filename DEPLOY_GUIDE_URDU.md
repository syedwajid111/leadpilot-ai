# LeadPilot AI — Vercel par live karne ki guide

Kharcha: **zero** (Vercel free + Neon free + Gemini free). Waqt: takreeban 30 minute.

## Step 1 — GitHub par upload (10 min)
1. github.com → **New repository** → naam `leadpilot-ai` → Private ya Public dono chalenge → **Create**
2. Zip extract karein. `leadpilot` folder ke **andar** jo kuch hai (app, components, lib, package.json …) wo upload karna hai.
3. Repo page par **"uploading an existing file"** → saari files aur folders ko **mouse se drag & drop** karein (file picker se folders nahi jaate).
4. **Commit changes**.
5. Check karein ke `app`, `components`, `lib` folders repo mein nazar aa rahe hain. Agar folders nahi gaye to **GitHub Desktop** app se upload karein (ye hamesha poora folder bhejta hai).

## Step 2 — Vercel se connect (5 min)
1. vercel.com → GitHub se login → **Add New → Project** → `leadpilot-ai` ke saamne **Import**
2. Framework khud **Next.js** select hoga. Kuch change na karein.
3. **Environment Variables** khol ke ye 2 add karein:
   - `GEMINI_API_KEY` = aap ki Gemini key
   - `ADMIN_PASSWORD` = apna koi mazboot password (dashboard ke liye)
4. **Deploy** dabayein. 1–2 minute mein link mil jayega, jaise `leadpilot-ai.vercel.app`

## Step 3 — Database (5 min, zaroori)
Database ke baghair leads thori der baad ghayab ho jati hain.
1. Vercel project → **Storage** tab → **Create Database** → **Neon** (free plan) → **Continue**
2. Region: **Singapore** ya jo qareeb ho → Create → project se **Connect** karein
3. Ye khud `DATABASE_URL` add kar deta hai.
4. **Deployments** tab → sab se upar wali deployment → **⋯ → Redeploy**
5. Tables app khud bana leti hai, kuch aur nahi karna.

## Step 4 — Apna domain (10 min + DNS ka intezaar)
1. Vercel project → **Settings → Domains** → likhein `fyp.aapkadomain.com` → **Add**
2. Vercel ek **CNAME** record dikhayega. Jo value Vercel dikhaye wahi use karein.
3. Hostinger **hPanel → Domains → DNS / Nameservers → DNS records**:
   - Type: **CNAME** · Name: **fyp** · Target: jo Vercel ne dikhaya · Add
   - Agar `fyp` naam ka koi purana A ya CNAME record hai to pehle use delete karein
4. 5–30 minute mein Vercel par **Valid Configuration** aa jayega. SSL (https) khud lag jata hai.

## Step 5 — Test
- Site kholein → chat mein likhein "I need a website" → poori baat karein → slot book karein
- `/admin` kholein → password daalein → aap ki lead score ke saath nazar aayegi
- **Load demo leads** dabayein → presentation ke liye 6 sample leads aa jayengi
- Kisi lead par **Write summary and follow-up email** dabayein
- Dashboard ke upar **"AI: Gemini connected"** aur **"Data: Neon Postgres"** likha hona chahiye

## Masle aur hal
| Masla | Hal |
|---|---|
| Dashboard par "AI: offline mode" | `GEMINI_API_KEY` ka naam bilkul sahi likhein, phir Redeploy |
| "No database connected" warning | Step 3 dobara karein, phir Redeploy |
| Build fail | Vercel → Deployments → failed wali → **Build Logs** ka screenshot bhejein |
| Domain par "Invalid configuration" | DNS mein CNAME ka Name sirf `fyp` ho (poora domain nahi), aur thora intezaar karein |
| Chat ke jawab simple/robotic hain | Gemini key ka quota khatam ho sakta hai; Groq ki free key `GROQ_API_KEY` bhi add kar dein |

## Apni agency ke liye use karna
`lib/knowledge.ts` mein naam, services, packages aur prices badal dein. Agent wahi bechega.
