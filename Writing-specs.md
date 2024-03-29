Here is a checklist to help with writing specs.

- [ ] List the team who is assigned including QA, Designer, PM, and devs per platform.
- [ ] Add an objective - Generic description of what's being planned.
- [ ] Add the status of the spec: `Pre-draft` (not ready for review), `Draft`, `In Development`, or `Complete` which signals that it is landed on Nightly.
- [ ] How does the feature relate to high level objectives of the company.
- [ ] Non-goals of the spec.
- [ ] Target platforms that will be supported (e.g. Desktop, iOS, Android, or which sites it applies to etc.)
- [ ] Does clearing browsing data affect the thing being spec'ed?
- [ ] Does the thing being spec'ed change with different window types? E.g. Private window and Tor window?
- [ ] Will the feature be available on all channels? Is a feature flag needed so that work can land incrementally without reaching Release channel until it's ready?
- [ ] Are there any open questions? List them explicitly. 
- [ ] What are the states of what you are designing?
- [ ] Which state is persistent and which state is not.
- [ ] Did you specify not only how things should be but what has to change from the current way?
- [ ] Can a time estimation be provided? 
- [ ] Are things consistent with design guidelines that exist? 
- [ ] Are there conflicting in-progress specs that should be considered?
- [ ] Are acronyms being used defined somewhere? 
- [ ] Are the strings defined that will be used? Remember to follow up after seeing real builds and get all string changes in by the time it is on Dev channel.
- [ ] Does your spec mention a specific version? In most cases this shouldn't be done, it's ok to drive for a specific version but most things should ride the trains.
- [ ] Are there any Privacy-Preserving Product Analytics (P3A) needs? 
- [ ] Have you considered accessibility? You should, specify any relevant details. 
- [ ] Is every error condition possible along with how to handle them spelt out explicitly?

If there are UI component
- [ ] Do you have mockups for every view and every state?
- [ ] Did you specify dimensions?
- [ ] Did you specify color values?
- [ ] Did you specify how it works responsively?
- [ ] Did you specify if these things are different per platform?
- [ ] If there are links, make sure a plan is in place to get the documentation created before the code lands.

If there are technical components
- [ ] Provide technical information when possible, work with a developer if needed.

Privacy / security
- [ ] Is there any kind of pings being made to a remote server?
- [ ] Is there any encryption being done?
- [ ] Is any information being hashed?
- [ ] Is there privacy or security sensitive information being persisted?
- [ ] Does anything make you think the security or privacy team might be interested in the work?
- [ ] Did you file a security / privacy review if any of the above are true?

Devops involvement
- [ ] Does the spec need to use a service?
- [ ] Does the spec list anything that needs to be downloaded and possibly be behind a CDN?
- [ ] Are there things that will need ongoing process or maintenance that could be added to Jenkins?
- [ ] Does the change need to proxy any network traffic?
- [ ] Did you file a devops issue if any of the above are true?

Process considerations
- [ ] Post the specs for review on #specs.
- [ ] Callout major status changes when the draft enters a new status.
- [ ] Specs should be updated forever unless there is documentation that exists. Then a spec can be a diff on the documentation.
- [ ] Can the work be done in iterations or phases? If so you might want to indicate priority on things within the spec or consider splitting up the spec. 
- [ ] Once work is about to begin, schedule a kick-off meeting to start the work.
- [ ] Push to make sure tests are defined.
- [ ] Is a QA plan defined?