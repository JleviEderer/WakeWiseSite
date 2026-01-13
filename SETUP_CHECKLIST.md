# WakeWise Site Setup Checklist

## Step 1: Register Domain on Cloudflare (~5 min)

1. Go to [Cloudflare Registrar](https://dash.cloudflare.com/?to=/:account/domains/register)
2. Create account if needed (free)
3. Search for your domain (e.g., `wakewise.app`, `wakewise.io`, `getwakewise.com`)
4. Purchase the domain (~$10-15/year depending on TLD)
5. Wait for registration to complete (usually instant)

## Step 2: Set Up Email Routing on Cloudflare (~10 min)

1. In Cloudflare dashboard, click on your new domain
2. Go to **Email** → **Email Routing**
3. Click **Enable Email Routing**
4. Add a destination address:
   - Click **Destination addresses**
   - Add your personal Gmail (e.g., `jleviederer@gmail.com`)
   - Verify it by clicking the link sent to your Gmail
5. Create a routing rule:
   - Click **Routing rules** → **Create address**
   - Custom address: `contact` (this creates contact@yourdomain.com)
   - Destination: Select your verified Gmail
   - Click **Save**
6. (Optional) Create additional addresses like `justin@yourdomain.com`

### Send FROM your custom email via Gmail:

1. In Gmail, go to **Settings** (gear icon) → **See all settings**
2. Go to **Accounts and Import** tab
3. Under "Send mail as", click **Add another email address**
4. Enter your name and new email (e.g., `contact@wakewise.app`)
5. Uncheck "Treat as an alias"
6. For SMTP server, use Gmail's:
   - SMTP: `smtp.gmail.com`
   - Port: `587`
   - Username: your Gmail address
   - Password: your Gmail app password (create one at https://myaccount.google.com/apppasswords)
7. Verify with the code sent to your Cloudflare-forwarded email

## Step 3: Deploy Site to Vercel (~5 min)

### Option A: Deploy via GitHub (Recommended)

1. Create a new repo on GitHub called `wakewise-site`
2. Push this folder to GitHub:
   ```bash
   cd C:\Users\justi\OneDrive\wakewise-site
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/YOUR_USERNAME/wakewise-site.git
   git push -u origin main
   ```
3. Go to [Vercel](https://vercel.com) and sign in with GitHub
4. Click **Add New** → **Project**
5. Import your `wakewise-site` repository
6. Click **Deploy** (no configuration needed for static HTML)

### Option B: Deploy via Vercel CLI

```bash
npm i -g vercel
cd C:\Users\justi\OneDrive\wakewise-site
vercel
```

## Step 4: Connect Custom Domain to Vercel (~5 min)

1. In Vercel dashboard, go to your project
2. Click **Settings** → **Domains**
3. Add your domain (e.g., `wakewise.app`)
4. Vercel will show you DNS records to add
5. Go back to Cloudflare → **DNS**
6. Add the records Vercel shows (usually CNAME or A records)
7. Wait for propagation (usually 1-5 minutes)
8. Vercel will auto-provision SSL

## Step 5: Reapply to Garmin

Once everything is live, reapply to Garmin Connect Developer Program with:

- **Website**: `https://wakewise.app` (or your domain)
- **Privacy Policy**: `https://wakewise.app/privacy-policy.html`
- **Email**: `contact@wakewise.app` (or `firstname.lastname@yourdomain.com`)

Make sure to use your custom domain email, not Gmail!

---

## Quick Reference

| Service | Purpose | Cost |
|---------|---------|------|
| Cloudflare | Domain + Email routing | ~$10-15/yr for domain |
| Vercel | Website hosting | Free |
| Gmail | Email backend | Free |

## Troubleshooting

**Email not arriving?**
- Check Cloudflare Email Routing is enabled
- Verify destination address in Cloudflare
- Check spam folder

**Site not loading on custom domain?**
- DNS propagation can take up to 48hrs (usually faster)
- Verify DNS records match what Vercel shows
- Try clearing browser cache or using incognito

**Vercel SSL not working?**
- Make sure DNS is pointed correctly
- Wait a few minutes for auto-provisioning
