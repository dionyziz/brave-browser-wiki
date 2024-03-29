Feel free to copy this into an issue if you want to keep track of items per-milestone.
Be super sure that <version> is replaced with the version you wish to use.

### Prerequisites

- [ ] Check Tor is up to date with its latest upstream.
- [ ] At freeze date, consult with the security team to ensure that all security issues have been included.
- [ ] At freeze date, consult with PR team (@catherinecorre) and provide heads up on release timing, screenshots, other deliverables.

### Release Notes to Staging
- [ ] Mark closed issues in github as release-notes/exclude or release-notes/include.
- [ ] Commit release notes to [CHANGELOG.md](https://github.com/brave/brave-browser/blob/master/CHANGELOG.md) in brave-browser master branch, must be completed before release to production Jenkins build job is run.
- [ ] Stage release notes to https://github.com/brave/brave-browser/releases/

### Certification and Builds
- [ ] Upload builds to Omaha test channels (`86-r-test`, `64-r-test`, `test`(mac))
- [ ] Log into Fastly, clear CDN cache for: `updates-cdn.bravesoftware.com`, `updates.bravesoftware.com`

### Test Staging for Updates
- [ ] Install a prior version of Brave and update via `test` channels (`86-r-test`, `64-r-test`, `test`(macOS))
   - [ ] Confirm version matches expectations
- [ ] QA summary and sign off report under #release via Slack.

### Release to production download locations
- [ ] Publish github release (remove 'pre-release' checkmark)
- [ ] Upload Mac/Win build to Omaha production channels (`x86-rel`, `x64-rel`, `stable`(mac))
- [ ] Sign Linux builds and upload to S3 repositories
- [ ] Upload Mac `.dmg` and `.pkg` to S3 bucket (i.e. `aws s3 cp ./Brave-Browser-Dev.dmg s3://brave-browser-downloads/latest/Brave-Browser-Dev.dmg --acl public-read`)
- [ ] Upload Windows stub and silent installer to S3 bucket using similar command to Mac dmg above (i.e `BraveBrowserSetup.exe`, `BraveBrowserSetup32.exe`, `BraveBrowserSilentSetup.exe`, `BraveBrowserSilentSetup32.exe`)

### Clear Production Fastly cache
- [ ] Log into Fastly, clear CDN cache for: `brave-browser-downloads.s3.brave.com`, `brave-browser-apt-release.s3.brave.com`, `brave-browser-rpm-release.s3.brave.com`, `updates-cdn.bravesoftware.com`, `updates.bravesoftware.com`

### Updates Testing on Production
- [ ] Wait for confirmation that Windows live update works
- [ ] Wait for confirmation that macOS live update works
- [ ] Wait for confirmation that Linux live update works

### Download & Install Binaries from Brave.com
- [ ] download binary from https://brave.com on `Win x64`
   - should be using `https://laptop-updates.brave.com/latest/winx64`
- [ ] download binary from https://brave.com on `Win x86`
   - should be using `https://laptop-updates.brave.com/latest/winia32`
- [ ] download binary from https://brave.com on `macOS`
   - should be using `https://laptop-updates.brave.com/latest/osx`
- [ ] download the `.exe` binary from a referral page (Production) on `Win x64`
   - check `brave://local-state` and ensure the `promoCode` is being listed
- [ ] download the `.exe` binary from a referral page (Production) on `Win x86`
   - check `brave://local-state` and ensure the `promoCode` is being listed
- [ ] download the `.pkg` binary from a referral page (Production) on `macOS`
   - check `brave://local-state` and ensure the `promoCode` is being listed

### Announcements
- [ ] Publish the release notes to `GitHub`
- [ ] Publish the release notes to `https://www.brave.com/latest`
- [ ] Announce release on https://community.brave.com/ (@Hollons)
- [ ] Announce release on https://www.reddit.com/r/brave_browser/ (@Hollons)
- [ ] Notify #announcements, #community of the latest release with a link to the release notes

### Update Release channel wiki
- [ ] Update entries here as needed: https://github.com/brave/brave-browser/wiki/Brave-Release-Schedule

### Closing milestones
- [ ] Set a release date and close the appropriate milestone under https://github.com/brave/brave-browser/milestones
- [ ] Set a release date and close the appropriate milestone under https://github.com/brave/brave-core/milestones