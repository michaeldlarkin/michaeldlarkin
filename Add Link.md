<%*
// Prompt for a URL (prefilled from the clipboard), fetch the page's metadata,
// let you edit the title, then insert a card-link block plus the visible URL.
const clip = ((await tp.system.clipboard()) || "").trim();
let url = ((await tp.system.prompt("URL", clip.startsWith("http") ? clip : "")) || "").trim();

if (url) {
  if (!/^https?:\/\//i.test(url)) url = "https://" + url;

  let html = "";
  try {
    const res = await tp.obsidian.requestUrl({ url: url, headers: { "User-Agent": "Mozilla/5.0" } });
    html = res.text || "";
  } catch (e) {
    new tp.obsidian.Notice("Couldn't fetch page details; adding a basic card.");
  }

  const decode = (s) => s
    .replace(/&amp;/g, "&").replace(/&quot;/g, '"').replace(/&#0?39;|&apos;/g, "'")
    .replace(/&lt;/g, "<").replace(/&gt;/g, ">").replace(/&nbsp;/g, " ")
    .replace(/\s+/g, " ").trim();

  const meta = (key) => {
    const val = "content=(?:\"([^\"]*)\"|'([^']*)')";
    const a = new RegExp("<meta[^>]*?(?:property|name)=[\"']" + key + "[\"'][^>]*?" + val, "i");
    const b = new RegExp("<meta[^>]*?" + val + "[^>]*?(?:property|name)=[\"']" + key + "[\"']", "i");
    const m = html.match(a) || html.match(b);
    return m ? decode(m[1] || m[2] || "") : "";
  };

  let host = "";
  try { host = new URL(url).hostname.replace(/^www\./, ""); } catch (e) {}

  const titleTag = html.match(/<title[^>]*>([\s\S]*?)<\/title>/i);
  const fetchedTitle = meta("og:title") || meta("twitter:title") || (titleTag ? decode(titleTag[1]) : "") || host || url;
  const title = ((await tp.system.prompt("Title (edit if you like)", fetchedTitle)) || fetchedTitle).trim();

  let description = meta("og:description") || meta("description") || meta("twitter:description");
  if (description.length > 200) description = description.slice(0, 197) + "...";

  let image = meta("og:image") || meta("twitter:image") || meta("twitter:image:src");
  if (image) { try { image = new URL(image, url).href; } catch (e) { image = ""; } }

  let favicon = "";
  try { favicon = new URL("/favicon.ico", url).href; } catch (e) {}

  const q = (s) => '"' + String(s).replace(/\\/g, "\\\\").replace(/"/g, '\\"') + '"';

  let block = "```cardlink\n";
  block += "url: " + q(url) + "\n";
  block += "title: " + q(title) + "\n";
  if (description) block += "description: " + q(description) + "\n";
  if (host) block += "host: " + q(host) + "\n";
  if (favicon) block += "favicon: " + q(favicon) + "\n";
  if (image) block += "image: " + q(image) + "\n";
  block += "```\n";
  block += "🔗 " + url + "\n\n";

  tR += block;
}
%>