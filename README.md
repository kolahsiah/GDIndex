# GDIndex Dark Mode

<table style="width:100%;">
    <tr>
        <td><img src="http://github.gapchin.workers.dev/darkmode.jpg"></td>
        <td><img src="http://github.gapchin.workers.dev/darkmode_mobile.jpg"></td>
    </tr>
</table>

[繁體中文](README.zhtw.md)
[简体中文](README.zh.md)

> [GDIndex](https://github.com/maple3142/GDIndex) is similar to [GOIndex](https://github.com/donwa/goindex).
> It allows you to deploy a "Google Drive Index" on CloudFlare Workers along with many extra features
>
> By the way, instead of modify from GOIndex, this is a total rewrite

[Source](https://github.com/maple3142/GDIndex)

[Dark Mode Demo](https://github.gapchin.workers.dev/)

## Difference between GOIndex and GDIndex

-   Frontend is based on Vue.js
-   Image viewer doesn't require opening new page
-   Video player support subtitles(Currently only srt is supported)
-   Online PDF, EPUB reader
-   No directory-level password protection(.password)
-   Support Http Basic Auth
-   Support multiple drives(personal, team) without changing server's code
-   Only access directory need auth - [I change...](https://github.com/maple3142/GDIndex/issues/46#issuecomment-608016890) - Sub directories don't need auth

## Usage

### Simple and automatic way

Go [GDIndex Code Builder](https://gdrive.kolahsiah.repl.co/) and follow its instructions.

### Manual way

1. Install [rclone](https://rclone.org/)
2. Setup your Google Drive: https://rclone.org/drive/
3. Run `rclone config file` to find your `rclone.conf` location
4. Find `refresh_token` in your `rclone.conf`, and `root_folder_id` too(optionally).
5. Copy the content of [worker/dist/worker.js](worker/dist/worker.js) to CloudFlare Workers.
6. Fill `refresh_token`, `root_folder_id` and other options on the top of the script.
7. Deploy!

### Using service accounts

1. Create a service account, a corresponding service account key, and get the JSON from the [Google Cloud Platform console](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) 
2. In the props object, replace the `service_account_json` value with the contents of the service account JSON file and set `service_account` to `true`.
3. Make sure that the service account in question has access to the folder specified in `root_folder_id`
4. Deploy

## Lite mode

This mode will serve a simple nginx-like directory listing, and it only work with one drive. `upload` will be ignored in this mode.

On the top of the script, change `lite: false` into `lite: true`, than thats all.

To enable on-the-fly lite mode, especially with command-line applications, you can include a HTTP header `x-lite: true` in your requests.

[Lite mode demo](https://gdindex-demo-lite.maple3142.workers.dev/)
