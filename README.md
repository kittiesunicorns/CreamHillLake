# CHLA Website — Deployment Notes
# Cream Hill Lake Association — chlaweb.org
# HostGator account: home4 / cPanel user: unicorn

## File structure

chla/
├── index.html          Home page
├── events.html         Events calendar
├── rules.html          Rules & guidelines (waterfront / tennis / hours / bylaws)
├── gallery.html        Photo gallery
├── history.html        Club history
├── contact.html        Board & contact info
├── meta.json           Editable config — update board names, events, contact info here
├── css/
│   └── styles.css      All styles
├── img/
│   ├── fall_foliage.jpg
│   ├── old_clubhouse.jpg
│   ├── paddleboards.jpg
│   └── (add more photos here)
└── members/
    ├── index.html      Password-protected member portal
    ├── .htaccess       Locks the /members/ directory — DO NOT delete
    └── .htpasswd       Must be generated — see below


## Deploying to HostGator

1. Upload all files to: public_html/chlaweb.org/
   (or public_html/ if chlaweb.org is the primary domain)

2. Maintain the folder structure exactly as above.

3. The members/ folder is protected by .htaccess.
   The .htpasswd file must be generated before members can log in — see below.


## Setting up the members password

Option A — via cPanel (easiest):
  1. Log into cPanel at home4.hostgator.com
  2. Files > Directory Privacy
  3. Navigate to public_html/chlaweb.org/members
  4. Check "Password protect this directory"
  5. Set a username (e.g. "chlamember") and shared password
  6. cPanel creates .htpasswd automatically

Option B — command line:
  ssh into server, then:
    htpasswd -c /home/unicorn/public_html/chlaweb.org/members/.htpasswd chlamember
  Enter the shared password when prompted.

Note: The AuthUserFile path in .htaccess is:
  /home/unicorn/public_html/chlaweb.org/members/.htpasswd
Adjust this path if the domain lives in a different directory.


## Updating content

Board members / contact info:
  Edit meta.json OR edit contact.html directly.

Events:
  Edit events.html — copy/paste an existing .event-item block and update dates.

Gallery photos:
  Add jpg/png files to img/, then add <img> tags in gallery.html.
  Copy the existing gallery-item pattern.

Rules & bylaws:
  Edit rules.html — each rule is a .rule-item div.


## GitHub

Recommended: push to github.com/kittiesunicorns/CHLAwebsite
Deploy via .cpanel.yml the same way as the VLA and stopthewar sites.
