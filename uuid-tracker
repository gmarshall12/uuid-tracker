(function () {
  function getOrCreateUUID() {
    const key = 'visitor_uuid';
    let uuid = localStorage.getItem(key);

    if (!uuid) {
      uuid = ([1e7]+-1e3+-4e3+-8e3+-1e11).replace(/[018]/g, c =>
        (c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> c / 4).toString(16)
      );
      localStorage.setItem(key, uuid);
    }

    return uuid;
  }

  // Store UUID globally
  window.visitorUUID = getOrCreateUUID();

  // Append to outbound vendor links only
  document.addEventListener('DOMContentLoaded', () => {
    const vendorDomains = ['thrivelab.com', 'know.us', 'personanutrition.com'];
    const links = document.querySelectorAll('a[href]');

    links.forEach(link => {
      try {
        const url = new URL(link.href, window.location.origin);
        if (vendorDomains.includes(url.hostname)) {
          url.searchParams.set('ref_id', window.visitorUUID);
          link.href = url.toString();
        }
      } catch (e) {
        // Invalid or relative URLs (e.g. anchors or malformed hrefs)
      }
    });
  });
})();
