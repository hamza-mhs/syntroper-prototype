# Teams management · handoff for Murtaza

Agreed with Arsalan on 23 Nov 2026. Teams is the only new module cleared for development. Bounded context creation, use case creation and change specifications stay design-only for now.

Prototype: Codona_Prototype_final.html → left navigation → Teams (also Teams_Hierarchy_Prototype.html on its own).

## How it works

**Members come from the organization.** People join the org first, through Users (org-level invite by email). Teams never send invitations. A team only adds people who are already in the org.

**Adding members to a team.** Open a team card and press **Add members**. A list of org members who are not in the team opens inside the card, with a search box. Tick as many people as needed and press **Add N**. Everyone is added at once as Contributor; roles can then be changed per person. The list has an **Invite to org** link that goes to Users.

**Creating teams.** **Create Team** in the header is contextual: with a team open it reads *Create team in Engineering* and creates a sub-team under it; with nothing open it creates a top-level team. The **+** on hovering any card does the same for that card. A new team starts with a name only and no members.

**Archive, not delete.** The action is **Archive** everywhere (card and dialog). Archiving a team with sub-teams asks whether the sub-teams move up one level or are archived too. Archived teams can be restored later.

**Members as nodes.** Expanding a team shows every member as a node under the team card. Members form one column, stacked top to bottom and joined by a line; the team's sub-teams sit to the right of that column, each with its own member column when expanded (teams grow left to right, members top to bottom). For production, a layout library such as d3-hierarchy or ELK (layered) can apply the same rule. A member node has avatar, name, email and role; change the role from the role chip, or remove the person with × on hover. All members always show, never a subset, which fixes the old behaviour where some people appeared as cards and others were hidden. The chip on the connector reads e.g. **2 sub-teams · 3 members** and expands or collapses both. Org members who are in no team hang off the org card as “Org member · no team”.

**Default state.** Every team starts expanded, so all members and sub-teams are visible on first load. The chip under a card collapses it.

**Open card.** Clicking a card opens it in place: rename, members with role and remove, Add members, Sub-team, Move, Archive. Clicking empty canvas closes it and cancels a new team that hasn't been named.

**Canvas.** Pinch or ⌘/Ctrl + scroll zooms at the cursor, scroll or drag pans. Team cards are 272 px wide, member cards 212 px. Opening a card, expanding sub-teams, adding a team and adding members animate (about 0.25–0.3 s, off with reduced motion).

## Roles (static for now)

Super admin, Admin, Team admin, Architect, Contributor, Viewer. Roles are listed under **Roles**; editing which permissions each role has is out of scope for this round.

## Out of scope

Editable role permissions, business owners, billing and tiers.

## Also in this round

Canvas dots: brighter in dark mode, subtler in light mode (all dotted canvases).
