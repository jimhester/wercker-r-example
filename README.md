# Setup a new Application on [Wercker](https://app.wercker.com/)

- Goto https://app.wercker.com/#applications/create
- Step 4. Click wercker will checkout the code without using an SSH key
- Step 5. Ignore Step 5
- Step 6. If an open source project click 'Make my app public'
- Create
- Goto Settings
  - Scroll down to Infrastructure Stack
  - Select Ewok (5) from the dropdown.

# Code coverage reports with [Codecov](https://codecov.io)

- Add the new repository
- Copy your Codecov token (can be found later from Features -> Reveal repo token)
- In Wercker settings `Add new variable`.
  - Name: `CODECOV_TOKEN`
  - Value: paste the token value
  - Check `protected`
  - Save

# wercker.yml

The wercker.yml in this repository will automatically do the following.

- Retrieve all dependencies for your package
- Build and Check your package
- Run [lintr](https://github.com/jimhester/lintr)
- Run [covr](https://github.com/jimhester/covr) and upload results to [Codecov](https://codecov.io).

If you do not want one or more of the above simply remove that step from the file.

# .Rbuildignore

Add the following lines to .Rbuildignore.  Otherwise the package check will produce a  "Non-standard file/directory found" note.
```
^wercker\.yml$
^shim_package\.sh$
^unshim_package\.sh$
```

For more information on available options for each step see their pages on the
[Wercker Registry](https://app.wercker.com/#search/steps/jimhester).

The base image for this file is `rocker/hadleyverse` which contains a number of
common packages.  For optimum build time and storage size you are encouraged to
create a custom docker container containing only the dependencies for your
package.
