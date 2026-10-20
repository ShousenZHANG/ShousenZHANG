# CLAUDE.md

## Repository purpose

This is the GitHub profile repository for `ShousenZHANG`. GitHub renders `README.md` on the profile. There is no application, package manager, build step, or test suite.

## README design

Keep the profile compact and text-first, with three left-aligned Markdown paragraphs:

1. A bold positioning phrase followed by the technical scope in the same paragraph.
2. A concise contributor credit linking to Dify and Haystack, with each project's star count in plain-text parentheses.
3. Portfolio, LinkedIn, and Email links separated by middle dots, all at normal body size.

The sidebar already supplies the name and biography. Pinned repositories supply detailed project evidence. Keep the README under approximately ten rendered lines at a 320px viewport.

Use native GitHub Markdown and natural wrapping. Let GitHub supply typography, colors, link states, and theme support. Keep meaningful text selectable and accessible, with descriptive links. The owner prefers a compact developer introduction over a centered hero or oversized heading.

Preserve the minimal direction: no layout tables, image banners, badge walls, statistics widgets, animations, or duplicated project descriptions. The README has no Joblit link.

Concrete claims need public evidence. The owner explicitly requests project star counts beside the contributor credit. Verify them against the GitHub API, round to one decimal with a `k` suffix, and record the verification date in an HTML comment. Use plain text instead of badges. Star counts belong to the linked projects and do not measure the owner's contributions.

## Editing and verification

- Compare local and remote README content before editing; preserve newer owner-authored content.
- Preview with GitHub's Markdown renderer and GitHub styles. Check the profile context as well as the isolated README.
- Check light and dark themes, 320px and 375px widths, natural wrapping, readable links, and keyboard focus. Confirm that the README introduces no horizontal overflow.
- Verify retained destinations. Record any site that blocks automated verification instead of claiming it passed.
- Run `git diff --check`. Use Conventional Commits if a commit is requested.
