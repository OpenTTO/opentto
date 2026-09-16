# OpenTTO.com setup

This site is intentionally a static website: no database, accounts, cookies, uploads, API keys, or server-side processing.

## 1. Confirm the configured links

The site is already configured with:

- OpenTTO CryptPad interest form: `https://cryptpad.fr/form/#/2/form/view/88EqqswXGeGkx-lrVHMpv9ajL1V1bOeFqaxE7c9paB4/`
- OpenTTO GitHub repository: `https://github.com/OpenTTO/opentto/`

No link replacement is required before launch.

## 2. Put these files in the website repository

Upload the **contents** of this package to the root of the repository, not the enclosing `opentto-website` folder.

The repository root should contain:

    index.html
    styles.css
    CNAME
    .nojekyll
    README.md
    SETUP.md
    assets/

## 3. Enable GitHub Pages

In the website repository:

1. Open **Settings**.
2. Select **Pages** under "Code and automation."
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select branch **main** and folder **/(root)**.
5. Click **Save**.

If this is a GitHub Free account/organization, the Pages repository needs to be public. GitHub's paid plans support Pages from private repositories. The website itself is intended to be public either way.

## 4. Verify opentto.com in GitHub before changing DNS

GitHub recommends verifying a custom domain to reduce takeover risk.

For an organization, go to the organization's settings and find the Pages/domain verification area. Add `opentto.com`. GitHub will give you a DNS TXT record.

In Namecheap:

1. Domain List → `opentto.com` → **Manage**.
2. **Advanced DNS**.
3. Add the TXT record exactly as GitHub specifies.
4. Return to GitHub and complete verification after DNS propagates.

Leave that TXT verification record in place.

## 5. Add the custom domain in the repository

Repository → **Settings** → **Pages** → **Custom domain**.

Enter:

    opentto.com

and save it.

The included `CNAME` file already contains `opentto.com`. If GitHub updates that file for you, keep the GitHub-generated version.

## 6. Configure Namecheap DNS

In Namecheap → Domain List → `opentto.com` → Manage → Advanced DNS.

Remove conflicting parking, redirect, A, or CNAME records for `@` or `www` that would compete with GitHub Pages.

Add these four A records:

| Type | Host | Value |
|---|---|---|
| A Record | @ | 185.199.108.153 |
| A Record | @ | 185.199.109.153 |
| A Record | @ | 185.199.110.153 |
| A Record | @ | 185.199.111.153 |

Add:

| Type | Host | Value |
|---|---|---|
| CNAME Record | www | YOUR-GITHUB-OWNER.github.io |

Replace `YOUR-GITHUB-OWNER` with the GitHub user or organization that owns the Pages repository. Do **not** append the repository name.

Do not create a wildcard (`*`) DNS record.

DNS propagation can take time.

## 7. Enable HTTPS

After GitHub recognizes the DNS configuration and provisions the certificate:

Repository → Settings → Pages → check **Enforce HTTPS**.

GitHub may need some time to provision the certificate.

## 8. Test

Verify all of these:

- `https://opentto.com`
- `https://www.opentto.com`
- Join button opens the correct CryptPad form.
- GitHub button opens the intended OpenTTO repository/organization.
- Mobile layout works.
- Browser shows HTTPS without certificate warnings.

GitHub should redirect between the apex and `www` variants when both DNS configurations are correct.

## 9. Ongoing edits

Edit `index.html` or `styles.css`, commit to `main`, and GitHub Pages will republish the site. For collaborative work, use branches and pull requests rather than direct edits to `main`.

## Security boundary

Keep this public website static. Do not add institutional matter uploads, API keys, credentials, confidential agreements, invention disclosures, or other restricted information. If OpenTTO later runs AI workflows or accepts documents, treat that as a separate application/security architecture rather than adding it casually to this static site.
