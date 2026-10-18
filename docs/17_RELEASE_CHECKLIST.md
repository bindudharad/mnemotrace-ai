# 17. Release and Submission Readiness Checklist

## Code and reproducibility

- [ ] Fresh clone setup succeeds using README instructions.
- [ ] Exact dependencies are declared and lock strategy is documented.
- [ ] Tests pass on a clean environment.
- [ ] A minimal demo runs without hidden files or credentials.
- [ ] CI results correspond to the commit being submitted.
- [ ] No generated secrets, real personal data, or local databases are committed.

## Security

- [ ] Denied action cannot reach the mock sink.
- [ ] Quarantined record cannot be returned by normal reads.
- [ ] Unknown principal and missing policy fail safely.
- [ ] Checkpoint integrity failure prevents verified recovery.
- [ ] Replay rechecks policy and uses only approved synthetic events.
- [ ] Error paths do not disclose raw memory or secrets.
- [ ] Local server does not bind to public interfaces by default.

## Evaluation

- [ ] Scenario corpus version and hash recorded.
- [ ] Attack and benign cases are both present.
- [ ] Baselines and their controls are defined fairly.
- [ ] Metrics include raw numerator/denominator.
- [ ] Failures and unsupported attack classes are documented.
- [ ] All published scores come from a saved run report.

## Documentation and presentation

- [ ] README links work.
- [ ] `PROJECT_STATUS.md` matches implementation evidence.
- [ ] Change log and known limitations are current.
- [ ] Slide claims match the code that will be shown.
- [ ] “Proposed” vs “implemented” vs “verified” is explicit.
- [ ] Demo uses only synthetic data and mocked external actions.
- [ ] Original contribution is clearly explained.
- [ ] Third-party license and attribution obligations are satisfied.

## Submission-day preflight

- [ ] Restart laptop and run the demo from scratch.
- [ ] Bring an offline recording/screenshot fallback and a local copy of scenario fixtures.
- [ ] Confirm network-independent path works if Wi-Fi fails.
- [ ] Prepare 30-second, 90-second, and 3-minute explanations.
- [ ] Know the limitations and be prepared to explain how results were measured.
