# GPX Track Poster with GitHub Actions Automation

*Based on [flopp/GpxTrackPoster](https://github.com/flopp/GpxTrackPoster) with custom GitHub Actions workflow*

Automatically generate beautiful activity posters from your Strava data using GitHub Actions. This fork runs daily to create 5 different poster styles and pushes them to a dedicated `output` branch.

## 🚀 Quick Setup

### 1. Get Strava Credentials

*Strava setup instructions adapted from [GitHubPoster](https://github.com/yihong0618/GitHubPoster/tree/main?tab=readme-ov-file#strava)*

<details>

1. Sign in/Sign up [Strava](https://www.strava.com/) account
2. Open after successful Signin [Strava Developers](http://developers.strava.com) -> [Create & Manage Your App](https://strava.com/settings/api)

3. Create `My API Application`: Enter the following information

<br>

![My API Application](https://raw.githubusercontent.com/shaonianche/gallery/master/running_page/strava_settings_api.png)
Created successfully：

<br>

![](https://raw.githubusercontent.com/shaonianche/gallery/master/running_page/created_successfully_1.png)

4. Use the link below to request all permissions: Replace `${your_id}` in the link with `My API Application` `Client ID`
```
https://www.strava.com/oauth/authorize?client_id=${your_id}&response_type=code&redirect_uri=http://localhost/exchange_token&approval_prompt=force&scope=read_all,profile:read_all,activity:read_all,profile:write,activity:write
```
![get_all_permissions](https://raw.githubusercontent.com/shaonianche/gallery/master/running_page/get_all_permissions.png)

5. Get the `code` value in the link

<br>

example：
```
http://localhost/exchange_token?state=&code=1dab37edd9970971fb502c9efdd087f4f3471e6e&scope=read,activity:write,activity:read_all,profile:write,profile:read_all,read_all
```
`code` value：
```
1dab37edd9970971fb502c9efdd087f4f3471e6
```
![get_code](https://raw.githubusercontent.com/shaonianche/gallery/master/running_page/get_code.png)

6. Use `Client_id`、`Client_secret`、`Code` get `refresch_token`: Execute in `Terminal/iTerm`
```
curl -X POST https://www.strava.com/oauth/token \
-F client_id=${Your Client ID} \
-F client_secret=${Your Client Secret} \
-F code=${Your Code} \
-F grant_type=authorization_code
```
example：
```
curl -X POST https://www.strava.com/oauth/token \
-F client_id=12345 \
-F client_secret=b21******d0bfb377998ed1ac3b0 \
-F code=d09******b58abface48003 \
-F grant_type=authorization_code
```
</details>

### 2. Fork this repository

### 3. Set GitHub Secrets

Add these secrets to your forked repository:

| Secret | Description |
|--------|-------------|
| `STRAVA_CLIENT_ID` | Strava API Client ID |
| `STRAVA_CLIENT_SECRET` | Strava API Client Secret |
| `STRAVA_REFRESH_TOKEN` | Strava Refresh Token |
| `ACTIVITY_TYPE` | Optional activity filter (e.g., "Run") |

## 📁 Generated Files

Posters are generated daily in the `output` branch:

```
output/
├── strava_grid.svg
├── strava_calendar.svg
├── strava_github.svg
├── strava_circular.svg
└── strava_heatmap.svg
```
#### Grid Poster (--type grid)

![Grid Poster](https://raw.githubusercontent.com/a11might/GpxTrackPoster/output/strava_grid.svg)

#### Calendar Poster (--type calendar)

![Calendar Poster](https://raw.githubusercontent.com/a11might/GpxTrackPoster/output/strava_calendar.svg)

#### Github Poster (--type github)

![Github Poster](https://raw.githubusercontent.com/a11might/GpxTrackPoster/output/strava_github.svg)

#### Circular Poster (--type circular)

![Circular Poster](https://raw.githubusercontent.com/a11might/GpxTrackPoster/output/strava_circular.svg)

#### Heatmap Poster (--type heatmap)

![Heatmap Poster](https://raw.githubusercontent.com/a11might/GpxTrackPoster/output/strava_heatmap.svg)

## ⚙️ Customization

Edit `.github/workflows/run_poster_generate.yml`:
- Change schedule: modify cron expression
- Adjust colors: update `--track-color` parameters
- Remove poster types: comment out unwanted steps

## 🔍 Manual Trigger

You can also manually run the workflow from the Actions tab in your GitHub repository.

## 📄 License

This project follows the original [MIT License](https://github.com/flopp/GpxTrackPoster/blob/master/LICENSE).