# Issues

GitHub Issues i `pissmyran/bastion_windows` är repots ärendehantering.

## Arbetssätt

- Läs hela ärendet före arbete: text, etiketter, kommentarer och kopplade pull requests.
- Ett ärende ska beskriva ett sammanhållet problem, med acceptanskriterier och hinder i texten.
- Beslut som ska bestå skrivs in i dokumentationen, inte bara i en kommentar.

## Från en molnsession

`gh issue` fungerar inte i molnsessioner (GraphQL är avstängt). Använd REST:

- Läs: `gh api repos/pissmyran/bastion_windows/issues/<n>` och `…/issues/<n>/comments`
- Lista öppna: `gh api 'repos/pissmyran/bastion_windows/issues?state=open'`
- Skapa: `gh api repos/pissmyran/bastion_windows/issues -f title='…' -f body='…'`
- Kommentera: `gh api repos/pissmyran/bastion_windows/issues/<n>/comments -f body='…'`
- Stäng: `gh api -X PATCH repos/pissmyran/bastion_windows/issues/<n> -f state=closed`
