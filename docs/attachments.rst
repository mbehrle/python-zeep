============================
SOAP Attachments (multipart)
============================

If the server responds with a Content-type: multipart, a MessagePack object
will be returned. It contains a root object and a number of attachments.

Example based on https://www.w3.org/TR/SOAP-attachments

.. code-block:: python

    from zeep import Client

    client = Client('http://www.risky-stuff.com/claim.svc?wsdl')

    pack = client.service.GetClaimDetails('061400a')

    ClaimDetails = pack.root
    SignedFormTiffImage = pack.attachments[0].data
    CrashPhotoJpeg = pack.attachments[1].data

    # Or lookup by content_id
    pack.get_by_content_id('<claim061400a.tiff@claiming-it.com>').data
