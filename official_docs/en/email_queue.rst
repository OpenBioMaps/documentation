.. _email-queue:

Email queue
***********

OpenBioMaps places supported outgoing email notifications in a project-scoped
queue. The :ref:`central background task worker <central-background-worker>`
sends them using the project's mail configuration. An email can remain queued
until the worker runs; queueing alone does not confirm delivery.

Project administrators with access to **Profile > Project administration >
Email queue** can inspect the queue for their project. The page shows counts by
status, the age of the oldest waiting email, and a table of recipients,
subjects, creation and next-attempt times, attempt counts, SMTP codes, and
last errors. Filter and sort the table to find a message. Use **Attempts** to
inspect its delivery history.

Statuses and actions
====================

``queued``
   Waiting for the first delivery attempt. **Cancel** is available.

``processing``
   Claimed by a worker. Wait for the outcome; no manual action is available.

``retry``
   A temporary failure is waiting for its next attempt. **Cancel** is
   available. The next-attempt time and last error help diagnose it.

``sent``
   The worker recorded a successful send. This does not prove that the
   recipient's mailbox accepted the email.

``failed``
   Delivery failed permanently or retries were exhausted. **Retry** is
   available only when the email is linked to a stored project message whose
   content can be restored.

``cancelled``
   The pending email was cancelled and will not be sent by the worker.

**Retry** requeues an eligible failed email and starts a new retry sequence.
**Cancel** applies only to ``queued`` and ``retry`` emails. Both actions affect
the selected email only. Message content is cleared after a terminal result;
old terminal task records are removed after the retention period.

Troubleshooting
===============

If email remains ``queued`` or ``retry``, check the
:ref:`background-worker service <central-background-worker>` and its logs.
Check the project's SMTP settings if attempts report connection or
authentication errors. Inspect **Attempts** and **Last error** before using
**Retry**. A worker interruption can lead to a repeated send, so verify the
recipient and message history when investigating duplicates.
