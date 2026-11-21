# DiaClean build of the piler image: upstream sutoj/piler plus current Ubuntu security updates.
#
# Why: sutoj/piler:1.4.9 (2026-06) ships php8.5 8.5.4-0ubuntu1.1. The PHP security release of
# 2026-11-19 (CVE-2026-129289 PHP-FPM request smuggling, CVE-2026-115560 sessions, CVE-2026-129474,
# CVE-2026-129182 and more) is backported by Ubuntu in 8.5.4-0ubuntu1.6 (resolute-security).
# Until upstream publishes a new image, this layer pulls in all pending Ubuntu updates.
ARG PILER_VERSION=1.4.9
FROM sutoj/piler:${PILER_VERSION}

ARG MIN_PHP_DEB=8.5.4-0ubuntu1.6

# hadolint ignore=DL3005
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get upgrade -y --no-install-recommends \
      -o Dpkg::Options::=--force-confold -o Dpkg::Options::=--force-confdef && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    v=$(dpkg-query -W -f='${Version}' php8.5-fpm) && \
    echo "php8.5-fpm $v" && \
    dpkg --compare-versions "$v" ge "$MIN_PHP_DEB" && \
    php -v | head -1
