## Documentation

This is a forked version of the [v-calendar plugin](https://github.com/nathanreyes/v-calendar). We've addressed accessibility issues in the calendar by adding aria labels in a few places. There is an [open PR here](https://github.com/nathanreyes/v-calendar/pull/1507/files) to merge these updates back into the original repo. The last PR that was merged into the original repo was in October of 2023, so I'm not holding my breath on that.

I wasn't able to figure out how the `lib` directory is built when a client runs `npm i --save v-calendar`. It didn't work out of the box. I tried doing it the proper way, by introducing a `prepare` script in package.json, but I never got it to work. So... I removed the `lib` line from `.gitignore` in the fork here and am just building the compiled lib code manually before pushing, tagging, and cutting a release. See below on how to do that if we need further updates:

```bash
# INITIALIZE
git clone git@github.com:slideroom/v-calendar.git; cd v-calendar
nvm use 16.16.0                         # i believe this is the latest working version
npm i

# CLIENT REPO: ATS
npm uninstall v-calendar
npm i <path-to-local-v-calendar-repo>   # install local version, then run ATS as you normally do

# DEV: V-CALENDAR
yarn build:lib                          # make updates, build, local ats env should automatically reload

# BUILD/DEPLOY: V-CALENDAR
npm run build
git commit -am 'YOUR UPDATE MSG'
git tag v2.4.4                          # update the tag as you like (as well as in commands below)
git push origin tag v2.4.4
# create a release off the tag          # https://github.com/slideroom/v-calendar/releases

# USE LATEST IN THE CLIENT: ATS
npm uninstall v-calendar
npm i git+https://git@github.com/slideroom/v-calendar.git#v2.4.4

```
