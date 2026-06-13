# Feature Catalog — Lobsters

> **Project:** Lobsters — a computing-focused community link aggregation site (https://github.com/lobsters/lobsters)
> **Generated:** 2026-06-13T00:00:00Z
> **Features:** 16

---

## Features

| # | Feature | Description | Key Files |
|---|---------|-------------|-----------|
| 1 | stories | Story submission, display, voting, saving, hiding, suggestions, and URL duplicate detection | 16 files |
| 2 | comments | Threaded commenting, voting, flagging, and reply notifications | 8 files |
| 3 | tags-categories | Tag and category management including user tag filtering | 7 files |
| 4 | home-feed | Homepage feeds: hottest, newest, active, recent, top, by-tag, by-domain, by-origin | 5 files |
| 5 | users | User profiles, invitation tree, banning, standing, and avatars | 6 files |
| 6 | authentication | Login, logout, two-factor authentication, and password reset | 4 files |
| 7 | signup-invitations | User registration, invitation system, and invitation requests | 8 files |
| 8 | settings | User settings including 2FA enrollment, Pushover, Mastodon, and GitHub integrations | 3 files |
| 9 | hats | User hat (flair) management and hat request workflow | 7 files |
| 10 | messages | Private messaging between users with email notifications | 6 files |
| 11 | inbox-notifications | Unified inbox for reply notifications and read tracking | 4 files |
| 12 | moderation | Moderation log, mod dashboard, flagged content, mod notes, bans, and mod tools | 19 files |
| 13 | mod-mail | Moderator group mail threads for internal mod communication | 10 files |
| 14 | search | Full-text search for stories and comments | 4 files |
| 15 | stats-about | Site statistics, about pages, privacy policy, chat info, and cabinet | 7 files |
| 16 | domains-origins | Domain and origin tracking for submitted story URLs | 3 files |

---

## File-to-Feature Mapping

```yaml
# PATTERNS:
#   - path/to/dir/          -> matches any file under that directory (recursive)
#   - path/to/prefix_*      -> glob wildcard, matches files with that prefix
#   - path/to/exact_file.rb -> exact file match

stories:
  - app/controllers/stories_controller.rb
  - app/controllers/story_image_controller.rb
  - app/controllers/story_urls_controller.rb
  - app/controllers/suggestions_controller.rb
  - app/models/story.rb
  - app/models/story_image.rb
  - app/models/story_text.rb
  - app/models/stories_paginator.rb
  - app/models/hidden_story.rb
  - app/models/saved_story.rb
  - app/models/link.rb
  - app/models/suggested_tagging.rb
  - app/models/suggested_title.rb
  - app/models/vote.rb
  - app/models/tagging.rb
  - app/helpers/stories_helper.rb
  - app/helpers/suggestions_helper.rb
  - app/jobs/create_story_card_job.rb
  - app/jobs/send_webmention_job.rb
  - app/views/stories/
  - app/views/suggestions/
  - app/views/saved/

comments:
  - app/controllers/comments_controller.rb
  - app/models/comment.rb
  - app/models/comment_stat.rb
  - app/models/comment_vote_hydrator.rb
  - app/models/read_ribbon.rb
  - app/mailers/email_reply_mailer.rb
  - app/jobs/notify_comment_job.rb
  - app/views/comments/
  - app/views/email_reply_mailer/

tags-categories:
  - app/controllers/tags_controller.rb
  - app/controllers/categories_controller.rb
  - app/models/tag.rb
  - app/models/tag_filter.rb
  - app/models/category.rb
  - app/views/tags/
  - app/views/categories/

home-feed:
  - app/controllers/home_controller.rb
  - app/controllers/filters_controller.rb
  - app/controllers/concerns/story_finder.rb
  - app/models/keystore.rb
  - app/views/home/
  - app/views/filters/

users:
  - app/controllers/users_controller.rb
  - app/controllers/avatars_controller.rb
  - app/models/user.rb
  - app/models/username.rb
  - app/models/inactive_user.rb
  - app/helpers/users_helper.rb
  - app/views/users/

authentication:
  - app/controllers/login_controller.rb
  - app/controllers/concerns/authenticatable.rb
  - app/mailers/password_reset_mailer.rb
  - app/views/login/
  - app/views/password_reset_mailer/

signup-invitations:
  - app/controllers/signup_controller.rb
  - app/controllers/invitations_controller.rb
  - app/models/invitation.rb
  - app/models/invitation_request.rb
  - app/mailers/invitation_mailer.rb
  - app/mailers/invitation_request_mailer.rb
  - app/views/signup/
  - app/views/invitations/
  - app/views/invitation_mailer/
  - app/views/invitation_request_mailer/

settings:
  - app/controllers/settings_controller.rb
  - app/models/mastodon_app.rb
  - app/views/settings/

hats:
  - app/controllers/hats_controller.rb
  - app/controllers/hat_requests_controller.rb
  - app/models/hat.rb
  - app/models/hat_request.rb
  - app/helpers/hats_helper.rb
  - app/views/hats/
  - app/views/hat_requests/

messages:
  - app/controllers/messages_controller.rb
  - app/models/message.rb
  - app/mailers/email_message_mailer.rb
  - app/jobs/notify_message_job.rb
  - app/mailboxes/inbox_mailbox.rb
  - app/views/messages/
  - app/views/email_message_mailer/

inbox-notifications:
  - app/controllers/inbox_controller.rb
  - app/models/notification.rb
  - app/mailboxes/backstop_mailbox.rb
  - app/views/inbox/

moderation:
  - app/controllers/moderations_controller.rb
  - app/controllers/banned_ips_controller.rb
  - app/controllers/mod/mod_controller.rb
  - app/controllers/mod/activities_controller.rb
  - app/controllers/mod/flagged_controller.rb
  - app/controllers/mod/notes_controller.rb
  - app/controllers/mod/comments_controller.rb
  - app/controllers/mod/stories_controller.rb
  - app/controllers/mod/domains_controller.rb
  - app/controllers/mod/domains_ban_controller.rb
  - app/controllers/mod/origins_controller.rb
  - app/controllers/mod/reparents_controller.rb
  - app/controllers/mod/tags_controller.rb
  - app/controllers/jobs_mod_controller.rb
  - app/models/moderation.rb
  - app/models/mod_activity.rb
  - app/models/mod_note.rb
  - app/models/flagged_commenters.rb
  - app/mailers/ban_notification_mailer.rb
  - app/views/moderations/
  - app/views/banned_ips/
  - app/views/mod/activities/
  - app/views/mod/flagged/
  - app/views/mod/notes/
  - app/views/mod/stories/
  - app/views/mod/domains/
  - app/views/mod/origins/
  - app/views/mod/reparents/
  - app/views/mod/tags/
  - app/views/ban_notification_mailer/

mod-mail:
  - app/controllers/mod_mails_controller.rb
  - app/controllers/mod_mail_messages_controller.rb
  - app/controllers/mod/mails_controller.rb
  - app/controllers/mod/mail_messages_controller.rb
  - app/models/mod_mail.rb
  - app/models/mod_mail_message.rb
  - app/models/mod_mail_recipient.rb
  - app/models/mod_mail_reference.rb
  - app/mailers/email_mod_mail_message_mailer.rb
  - app/jobs/notify_mod_mail_message_job.rb
  - app/views/mod_mails/
  - app/views/mod_mail_messages/
  - app/views/mod/mails/
  - app/views/mod/mail_messages/
  - app/views/email_mod_mail_message_mailer/

search:
  - app/controllers/search_controller.rb
  - app/models/search.rb
  - app/models/search_parser.rb
  - app/views/search/

stats-about:
  - app/controllers/stats_controller.rb
  - app/controllers/about_controller.rb
  - app/controllers/cabinet_controller.rb
  - app/models/stats.rb
  - app/helpers/cabinet_helper.rb
  - app/helpers/traffic_helper.rb
  - app/helpers/interval_helper.rb
  - app/views/stats/
  - app/views/about/
  - app/views/cabinet/

domains-origins:
  - app/controllers/origins_controller.rb
  - app/models/domain.rb
  - app/models/origin.rb
  - app/views/origins/
```

---

## Coverage

- **Controllers mapped:** 44 / 44 (excluding application_controller.rb)
- **Models mapped:** 42 / 42 (excluding application_record.rb, shared concerns, and short_id.rb)
- **Mailers mapped:** 7 / 7 (excluding application_mailer.rb)
- **Jobs mapped:** 5 / 9 (excluding base job and infrastructure jobs)
- **Helpers mapped:** 7 / 7 (excluding application_helper.rb)
- **Mailboxes mapped:** 2 / 2 (excluding application_mailbox.rb)
- **Unmapped files (infrastructure/shared, intentionally excluded):**
  - `app/controllers/application_controller.rb` — shared base controller
  - `app/models/application_record.rb` — shared base model
  - `app/models/concerns/email_blocklist_validation.rb` — shared validation concern
  - `app/models/concerns/token.rb` — shared token generation concern
  - `app/models/concerns/username_attribute.rb` — shared username concern
  - `app/models/short_id.rb` — shared utility module used across models
  - `app/helpers/application_helper.rb` — shared base helper
  - `app/mailers/application_mailer.rb` — shared base mailer
  - `app/jobs/application_job.rb` — shared base job
  - `app/jobs/fetch_email_blocklist_job.rb` — infrastructure maintenance job
  - `app/jobs/fetch_iana_tlds_job.rb` — infrastructure maintenance job
  - `app/jobs/mastodon_sync_list_job.rb` — infrastructure integration job
  - `app/jobs/restic_job.rb` — infrastructure backup job
  - `app/mailboxes/application_mailbox.rb` — shared base mailbox
  - `app/views/layouts/` — shared layout templates
  - `app/views/global/` — shared global partials
  - `app/views/helpers/` — shared view helper partials
  - `extras/` — shared utility libraries (markdowner, sponge, pushover, github, mastodon, etc.)
