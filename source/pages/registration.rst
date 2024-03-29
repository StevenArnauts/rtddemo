Registration
============

Process description of the eBox registration process

User flow
---------

User redirect
^^^^^^^^^^^^^^

When a user decides to register for the eBox, the HIP must redirect him to the registration endpoint at ``https://secure.doccle.be/kbc-ebox/register`` with the following query string parameters:

* **returnUrl**: After registration, the user will be sent back to your platform via this url
* **reference**: An identifier of the user in your system. This is can be used to link machine to machine messages to the correct user in your system.

.. note:: The return URL and reference must be url-safe encoded.

Example
^^^^^^^
::

    https://secure.doccle.be/kbc-ebox/register?returnUrl=https%3A%2F%2Fwww.yourdomain.be%2FEboxRegistrationCompleted&reference=XYZ

FAS log on and Consent Page
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The user will start registration process at the FAS. He will log in using any of the provided authentication methods: itsme, eID, ...

After authentication, the user agrees with the terms and conditions on the consent page. Note that the language of the FAS login page and consent page cannot be controlled by the eBox connector (not supported by FAS).

After registration
^^^^^^^^^^^^^^^^^^^

The user will be redirected back to the returnUrl you provided. The eBox connector will add a query string parameter with the result of the registration process:

* **status**: Reflects the outcome of the eBox registration process. Is always present and will have one these values: ``ok``, ``cancelled`` or ``failed``.
* **errorId**: a reference to the error that occured. Is only present when the status ``failed``. This can be used for debugging and error root cause analysis.


Backend flow
-------------

After a succesfull registration, the eBox connector will:

* synchronize document metadata between the Doccle receiver and eBox of the user
* post a ``registration completed`` event to your event api.


The body of the post request is formatted as a JSON string and contains:

* technicalSenderName
* receiverExternalReferenceId
* eventTimestamp
* citizenId
* eventType (``registration completed``)
* reference