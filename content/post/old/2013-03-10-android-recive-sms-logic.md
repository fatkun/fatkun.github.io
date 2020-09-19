---
title: android接收长短信处理逻辑
author: fatkun
type: post
date: 2013-03-10T13:14:08+00:00
url: /2013/03/android-recive-sms-logic.html
duoshuo_thread_id:
  - 6300410014041375490
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:39063:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
         * If this is the last part send the parts out to the application, otherwise
         * the part is stored for later processing. Handles both 3GPP concatenated messages
         * as well as 3GPP2 format WAP push messages processed by
         * {@link com.android.internal.telephony.cdma.CdmaSMSDispatcher#processCdmaWapPdu}.
         *
         * @param pdu the message PDU, or the datagram portion of a CDMA WDP datagram segment
         * @param address the originating address
         * @param referenceNumber distinguishes concatenated messages from the same sender
         * @param sequenceNumber the order of this segment in the message
         *          (starting at 0 for CDMA WDP datagrams and 1 for concatenated messages).
         * @param messageCount the number of segments in the message
         * @param timestamp the service center timestamp in millis
         * @param destPort the destination port for the message, or -1 for no destination port
         * @param isCdmaWapPush true if pdu is a CDMA WDP datagram segment and not an SM PDU
         *
         * @return a result code from {@link Telephony.Sms.Intents}, or
         *         {@link Activity#RESULT_OK} if the message has been broadcast
         *         to applications
         */</span>
        <span style="color: #000000; font-weight: bold;">protected</span> <span style="color: #000066; font-weight: bold;">int</span> processMessagePart<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">byte</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> pdu, <span style="color: #003399;">String</span> address, <span style="color: #000066; font-weight: bold;">int</span> referenceNumber,
                <span style="color: #000066; font-weight: bold;">int</span> sequenceNumber, <span style="color: #000066; font-weight: bold;">int</span> messageCount, <span style="color: #000066; font-weight: bold;">long</span> timestamp, <span style="color: #000066; font-weight: bold;">int</span> destPort,
                <span style="color: #000066; font-weight: bold;">boolean</span> isCdmaWapPush<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000066; font-weight: bold;">byte</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> pdus <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
            <span style="color: #003399;">Cursor</span> cursor <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #666666; font-style: italic;">// used by several query selection arguments</span>
                <span style="color: #003399;">String</span> refNumber <span style="color: #339933;">=</span> <span style="color: #003399;">Integer</span>.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span>referenceNumber<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #003399;">String</span> seqNumber <span style="color: #339933;">=</span> <span style="color: #003399;">Integer</span>.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span>sequenceNumber<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                <span style="color: #666666; font-style: italic;">// Check for duplicate message segment 检查有没有重复的片段，有就忽略了</span>
                cursor <span style="color: #339933;">=</span> mResolver.<span style="color: #006633;">query</span><span style="color: #009900;">&#40;</span>mRawUri, PDU_PROJECTION,
                        <span style="color: #0000ff;">&quot;address=? AND reference_number=? AND sequence=?&quot;</span>,
                        <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> <span style="color: #009900;">&#123;</span>address, refNumber, seqNumber<span style="color: #009900;">&#125;</span>, <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                <span style="color: #666666; font-style: italic;">// moveToNext() returns false if no duplicates were found</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>cursor.<span style="color: #006633;">moveToNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    Log.<span style="color: #006633;">w</span><span style="color: #009900;">&#40;</span>TAG, <span style="color: #0000ff;">&quot;Discarding duplicate message segment from address=&quot;</span> <span style="color: #339933;">+</span> address
                            <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; refNumber=&quot;</span> <span style="color: #339933;">+</span> refNumber <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; seqNumber=&quot;</span> <span style="color: #339933;">+</span> seqNumber<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #003399;">String</span> oldPduString <span style="color: #339933;">=</span> cursor.<span style="color: #006633;">getString</span><span style="color: #009900;">&#40;</span>PDU_COLUMN<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #000066; font-weight: bold;">byte</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> oldPdu <span style="color: #339933;">=</span> HexDump.<span style="color: #006633;">hexStringToByteArray</span><span style="color: #009900;">&#40;</span>oldPduString<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span><span style="color: #003399;">Arrays</span>.<span style="color: #006633;">equals</span><span style="color: #009900;">&#40;</span>oldPdu, pdu<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                        Log.<span style="color: #006633;">e</span><span style="color: #009900;">&#40;</span>TAG, <span style="color: #0000ff;">&quot;Warning: dup message segment PDU of length &quot;</span> <span style="color: #339933;">+</span> pdu.<span style="color: #006633;">length</span>
                                <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; is different from existing PDU of length &quot;</span> <span style="color: #339933;">+</span> oldPdu.<span style="color: #006633;">length</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #009900;">&#125;</span>
                    <span style="color: #000000; font-weight: bold;">return</span> Intents.<span style="color: #006633;">RESULT_SMS_HANDLED</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
                cursor.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                <span style="color: #666666; font-style: italic;">// not a dup, query for all other segments of this concatenated message</span>
                <span style="color: #003399;">String</span> where <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;address=? AND reference_number=?&quot;</span><span style="color: #339933;">;</span>
                <span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> whereArgs <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> <span style="color: #009900;">&#123;</span>address, refNumber<span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
                cursor <span style="color: #339933;">=</span> mResolver.<span style="color: #006633;">query</span><span style="color: #009900;">&#40;</span>mRawUri, PDU_SEQUENCE_PORT_PROJECTION, where, whereArgs, <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                <span style="color: #000066; font-weight: bold;">int</span> cursorCount <span style="color: #339933;">=</span> cursor.<span style="color: #006633;">getCount</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>cursorCount <span style="color: #339933;">!=</span> messageCount <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #666666; font-style: italic;">//如果不是最后一条，就插入raw表</span>
                    <span style="color: #666666; font-style: italic;">// We don't have all the parts yet, store this one away</span>
                    ContentValues values <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ContentValues<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    values.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;date&quot;</span>, timestamp<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    values.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;pdu&quot;</span>, HexDump.<span style="color: #006633;">toHexString</span><span style="color: #009900;">&#40;</span>pdu<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    values.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;address&quot;</span>, address<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    values.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;reference_number&quot;</span>, referenceNumber<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    values.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;count&quot;</span>, messageCount<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    values.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;sequence&quot;</span>, sequenceNumber<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>destPort <span style="color: #339933;">!=</span> <span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                        values.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;destination_port&quot;</span>, destPort<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #009900;">&#125;</span>
                    mResolver.<span style="color: #006633;">insert</span><span style="color: #009900;">&#40;</span>mRawUri, values<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #000000; font-weight: bold;">return</span> Intents.<span style="color: #006633;">RESULT_SMS_HANDLED</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
    &nbsp;
                <span style="color: #666666; font-style: italic;">// All the parts are in place, deal with them</span>
                pdus <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #000066; font-weight: bold;">byte</span><span style="color: #009900;">&#91;</span>messageCount<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> cursorCount<span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    cursor.<span style="color: #006633;">moveToNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #000066; font-weight: bold;">int</span> cursorSequence <span style="color: #339933;">=</span> cursor.<span style="color: #006633;">getInt</span><span style="color: #009900;">&#40;</span>SEQUENCE_COLUMN<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #666666; font-style: italic;">// GSM sequence numbers start at 1; CDMA WDP datagram sequence numbers start at 0</span>
                    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>isCdmaWapPush<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                        cursorSequence<span style="color: #339933;">--;</span>
                    <span style="color: #009900;">&#125;</span>
                    pdus<span style="color: #009900;">&#91;</span>cursorSequence<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> HexDump.<span style="color: #006633;">hexStringToByteArray</span><span style="color: #009900;">&#40;</span>
                            cursor.<span style="color: #006633;">getString</span><span style="color: #009900;">&#40;</span>PDU_COLUMN<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                    <span style="color: #666666; font-style: italic;">// Read the destination port from the first segment (needed for CDMA WAP PDU).</span>
                    <span style="color: #666666; font-style: italic;">// It's not a bad idea to prefer the port from the first segment for 3GPP as well.</span>
                    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>cursorSequence <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span> <span style="color: #339933;">&amp;&amp;</span> <span style="color: #339933;">!</span>cursor.<span style="color: #006633;">isNull</span><span style="color: #009900;">&#40;</span>DESTINATION_PORT_COLUMN<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                        destPort <span style="color: #339933;">=</span> cursor.<span style="color: #006633;">getInt</span><span style="color: #009900;">&#40;</span>DESTINATION_PORT_COLUMN<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #009900;">&#125;</span>
                <span style="color: #009900;">&#125;</span>
                <span style="color: #666666; font-style: italic;">// This one isn't in the DB, so add it</span>
                <span style="color: #666666; font-style: italic;">// GSM sequence numbers start at 1; CDMA WDP datagram sequence numbers start at 0</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>isCdmaWapPush<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    pdus<span style="color: #009900;">&#91;</span>sequenceNumber<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> pdu<span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
                    pdus<span style="color: #009900;">&#91;</span>sequenceNumber <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> pdu<span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
    &nbsp;
                <span style="color: #666666; font-style: italic;">// Remove the parts from the database</span>
                mResolver.<span style="color: #006633;">delete</span><span style="color: #009900;">&#40;</span>mRawUri, where, whereArgs<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">SQLException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                Log.<span style="color: #006633;">e</span><span style="color: #009900;">&#40;</span>TAG, <span style="color: #0000ff;">&quot;Can't access multipart SMS database&quot;</span>, e<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">return</span> Intents.<span style="color: #006633;">RESULT_SMS_GENERIC_ERROR</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">finally</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>cursor <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> cursor.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #666666; font-style: italic;">// Special handling for CDMA WDP datagrams</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>isCdmaWapPush<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #666666; font-style: italic;">// Build up the data stream</span>
                <span style="color: #003399;">ByteArrayOutputStream</span> output <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">ByteArrayOutputStream</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> messageCount<span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    <span style="color: #666666; font-style: italic;">// reassemble the (WSP-)pdu</span>
                    output.<span style="color: #006633;">write</span><span style="color: #009900;">&#40;</span>pdus<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span>, <span style="color: #cc66cc;">0</span>, pdus<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span>.<span style="color: #006633;">length</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
                <span style="color: #000066; font-weight: bold;">byte</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> datagram <span style="color: #339933;">=</span> output.<span style="color: #006633;">toByteArray</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                <span style="color: #666666; font-style: italic;">// Dispatch the PDU to applications</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>destPort <span style="color: #339933;">==</span> SmsHeader.<span style="color: #006633;">PORT_WAP_PUSH</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    <span style="color: #666666; font-style: italic;">// Handle the PUSH</span>
                    <span style="color: #000000; font-weight: bold;">return</span> mWapPush.<span style="color: #006633;">dispatchWapPdu</span><span style="color: #009900;">&#40;</span>datagram<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
                    pdus <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #000066; font-weight: bold;">byte</span><span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
                    pdus<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> datagram<span style="color: #339933;">;</span>
                    <span style="color: #666666; font-style: italic;">// The messages were sent to any other WAP port</span>
                    dispatchPortAddressedPdus<span style="color: #009900;">&#40;</span>pdus, destPort<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #000000; font-weight: bold;">return</span> Activity.<span style="color: #006633;">RESULT_OK</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #666666; font-style: italic;">// Dispatch the PDUs to applications</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>destPort <span style="color: #339933;">!=</span> <span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>destPort <span style="color: #339933;">==</span> SmsHeader.<span style="color: #006633;">PORT_WAP_PUSH</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    <span style="color: #666666; font-style: italic;">// Build up the data stream</span>
                    <span style="color: #003399;">ByteArrayOutputStream</span> output <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">ByteArrayOutputStream</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> messageCount<span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                        SmsMessage msg <span style="color: #339933;">=</span> SmsMessage.<span style="color: #006633;">createFromPdu</span><span style="color: #009900;">&#40;</span>pdus<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span>, getFormat<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                        <span style="color: #000066; font-weight: bold;">byte</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> data <span style="color: #339933;">=</span> msg.<span style="color: #006633;">getUserData</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                        output.<span style="color: #006633;">write</span><span style="color: #009900;">&#40;</span>data, <span style="color: #cc66cc;">0</span>, data.<span style="color: #006633;">length</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #009900;">&#125;</span>
                    <span style="color: #666666; font-style: italic;">// Handle the PUSH</span>
                    <span style="color: #000000; font-weight: bold;">return</span> mWapPush.<span style="color: #006633;">dispatchWapPdu</span><span style="color: #009900;">&#40;</span>output.<span style="color: #006633;">toByteArray</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
                    <span style="color: #666666; font-style: italic;">// The messages were sent to a port, so concoct a URI for it</span>
                    dispatchPortAddressedPdus<span style="color: #009900;">&#40;</span>pdus, destPort<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #666666; font-style: italic;">// The messages were not sent to a port</span>
                dispatchPdus<span style="color: #009900;">&#40;</span>pdus<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
            <span style="color: #000000; font-weight: bold;">return</span> Activity.<span style="color: #006633;">RESULT_OK</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #008000; font-style: italic; font-weight: bold;">/**
         * Dispatches standard PDUs to interested applications
         *
         * @param pdus The raw PDUs making up the message
         */</span>
        <span style="color: #000000; font-weight: bold;">protected</span> <span style="color: #000066; font-weight: bold;">void</span> dispatchPdus<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">byte</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> pdus<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            Intent intent <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Intent<span style="color: #009900;">&#40;</span>Intents.<span style="color: #006633;">SMS_RECEIVED_ACTION</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            intent.<span style="color: #006633;">putExtra</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;pdus&quot;</span>, pdus<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            intent.<span style="color: #006633;">putExtra</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;format&quot;</span>, getFormat<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            dispatch<span style="color: #009900;">&#40;</span>intent, RECEIVE_SMS_PERMISSION<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    /**
         * If this is the last part send the parts out to the application, otherwise
         * the part is stored for later processing. Handles both 3GPP concatenated messages
         * as well as 3GPP2 format WAP push messages processed by
         * {@link com.android.internal.telephony.cdma.CdmaSMSDispatcher#processCdmaWapPdu}.
         *
         * @param pdu the message PDU, or the datagram portion of a CDMA WDP datagram segment
         * @param address the originating address
         * @param referenceNumber distinguishes concatenated messages from the same sender
         * @param sequenceNumber the order of this segment in the message
         *          (starting at 0 for CDMA WDP datagrams and 1 for concatenated messages).
         * @param messageCount the number of segments in the message
         * @param timestamp the service center timestamp in millis
         * @param destPort the destination port for the message, or -1 for no destination port
         * @param isCdmaWapPush true if pdu is a CDMA WDP datagram segment and not an SM PDU
         *
         * @return a result code from {@link Telephony.Sms.Intents}, or
         *         {@link Activity#RESULT_OK} if the message has been broadcast
         *         to applications
         */
        protected int processMessagePart(byte[] pdu, String address, int referenceNumber,
                int sequenceNumber, int messageCount, long timestamp, int destPort,
                boolean isCdmaWapPush) {
            byte[][] pdus = null;
            Cursor cursor = null;
            try {
                // used by several query selection arguments
                String refNumber = Integer.toString(referenceNumber);
                String seqNumber = Integer.toString(sequenceNumber);
    
                // Check for duplicate message segment 检查有没有重复的片段，有就忽略了
                cursor = mResolver.query(mRawUri, PDU_PROJECTION,
                        &quot;address=? AND reference_number=? AND sequence=?&quot;,
                        new String[] {address, refNumber, seqNumber}, null);
    
                // moveToNext() returns false if no duplicates were found
                if (cursor.moveToNext()) {
                    Log.w(TAG, &quot;Discarding duplicate message segment from address=&quot; + address
                            + &quot; refNumber=&quot; + refNumber + &quot; seqNumber=&quot; + seqNumber);
                    String oldPduString = cursor.getString(PDU_COLUMN);
                    byte[] oldPdu = HexDump.hexStringToByteArray(oldPduString);
                    if (!Arrays.equals(oldPdu, pdu)) {
                        Log.e(TAG, &quot;Warning: dup message segment PDU of length &quot; + pdu.length
                                + &quot; is different from existing PDU of length &quot; + oldPdu.length);
                    }
                    return Intents.RESULT_SMS_HANDLED;
                }
                cursor.close();
    
                // not a dup, query for all other segments of this concatenated message
                String where = &quot;address=? AND reference_number=?&quot;;
                String[] whereArgs = new String[] {address, refNumber};
                cursor = mResolver.query(mRawUri, PDU_SEQUENCE_PORT_PROJECTION, where, whereArgs, null);
    
                int cursorCount = cursor.getCount();
                if (cursorCount != messageCount - 1) { //如果不是最后一条，就插入raw表
                    // We don't have all the parts yet, store this one away
                    ContentValues values = new ContentValues();
                    values.put(&quot;date&quot;, timestamp);
                    values.put(&quot;pdu&quot;, HexDump.toHexString(pdu));
                    values.put(&quot;address&quot;, address);
                    values.put(&quot;reference_number&quot;, referenceNumber);
                    values.put(&quot;count&quot;, messageCount);
                    values.put(&quot;sequence&quot;, sequenceNumber);
                    if (destPort != -1) {
                        values.put(&quot;destination_port&quot;, destPort);
                    }
                    mResolver.insert(mRawUri, values);
                    return Intents.RESULT_SMS_HANDLED;
                }
    
                // All the parts are in place, deal with them
                pdus = new byte[messageCount][];
                for (int i = 0; i &lt; cursorCount; i++) {
                    cursor.moveToNext();
                    int cursorSequence = cursor.getInt(SEQUENCE_COLUMN);
                    // GSM sequence numbers start at 1; CDMA WDP datagram sequence numbers start at 0
                    if (!isCdmaWapPush) {
                        cursorSequence--;
                    }
                    pdus[cursorSequence] = HexDump.hexStringToByteArray(
                            cursor.getString(PDU_COLUMN));
    
                    // Read the destination port from the first segment (needed for CDMA WAP PDU).
                    // It's not a bad idea to prefer the port from the first segment for 3GPP as well.
                    if (cursorSequence == 0 &amp;&amp; !cursor.isNull(DESTINATION_PORT_COLUMN)) {
                        destPort = cursor.getInt(DESTINATION_PORT_COLUMN);
                    }
                }
                // This one isn't in the DB, so add it
                // GSM sequence numbers start at 1; CDMA WDP datagram sequence numbers start at 0
                if (isCdmaWapPush) {
                    pdus[sequenceNumber] = pdu;
                } else {
                    pdus[sequenceNumber - 1] = pdu;
                }
    
                // Remove the parts from the database
                mResolver.delete(mRawUri, where, whereArgs);
            } catch (SQLException e) {
                Log.e(TAG, &quot;Can't access multipart SMS database&quot;, e);
                return Intents.RESULT_SMS_GENERIC_ERROR;
            } finally {
                if (cursor != null) cursor.close();
            }
    
            // Special handling for CDMA WDP datagrams
            if (isCdmaWapPush) {
                // Build up the data stream
                ByteArrayOutputStream output = new ByteArrayOutputStream();
                for (int i = 0; i &lt; messageCount; i++) {
                    // reassemble the (WSP-)pdu
                    output.write(pdus[i], 0, pdus[i].length);
                }
                byte[] datagram = output.toByteArray();
    
                // Dispatch the PDU to applications
                if (destPort == SmsHeader.PORT_WAP_PUSH) {
                    // Handle the PUSH
                    return mWapPush.dispatchWapPdu(datagram);
                } else {
                    pdus = new byte[1][];
                    pdus[0] = datagram;
                    // The messages were sent to any other WAP port
                    dispatchPortAddressedPdus(pdus, destPort);
                    return Activity.RESULT_OK;
                }
            }
    
            // Dispatch the PDUs to applications
            if (destPort != -1) {
                if (destPort == SmsHeader.PORT_WAP_PUSH) {
                    // Build up the data stream
                    ByteArrayOutputStream output = new ByteArrayOutputStream();
                    for (int i = 0; i &lt; messageCount; i++) {
                        SmsMessage msg = SmsMessage.createFromPdu(pdus[i], getFormat());
                        byte[] data = msg.getUserData();
                        output.write(data, 0, data.length);
                    }
                    // Handle the PUSH
                    return mWapPush.dispatchWapPdu(output.toByteArray());
                } else {
                    // The messages were sent to a port, so concoct a URI for it
                    dispatchPortAddressedPdus(pdus, destPort);
                }
            } else {
                // The messages were not sent to a port
                dispatchPdus(pdus);
            }
            return Activity.RESULT_OK;
        }
    
        /**
         * Dispatches standard PDUs to interested applications
         *
         * @param pdus The raw PDUs making up the message
         */
        protected void dispatchPdus(byte[][] pdus) {
            Intent intent = new Intent(Intents.SMS_RECEIVED_ACTION);
            intent.putExtra(&quot;pdus&quot;, pdus);
            intent.putExtra(&quot;format&quot;, getFormat());
            dispatch(intent, RECEIVE_SMS_PERMISSION);
        }</p></div>
    ";}
categories:
  - 未分类

---
长短信会分割成多条发送过来，每一条头部会带上总共有多少条，和这是第几条。（具体的细节我也没太深究）  
手机收到其中一条短信时，如果辨别出是长短信，则先把短信存储在raw表内(sqlite路径：/data/data/com.android.providers.telephony/databases/mmssms.db)  
当收完全部短信时，就把raw表的相关内容删除，传播到其他程序处理
贴代码充数。。。。o(╯□╰)o  
主要代码在SMSDispatcher.java里
<pre escaped="true" lang="java">/**
     * If this is the last part send the parts out to the application, otherwise
     * the part is stored for later processing. Handles both 3GPP concatenated messages
     * as well as 3GPP2 format WAP push messages processed by
     * {@link com.android.internal.telephony.cdma.CdmaSMSDispatcher#processCdmaWapPdu}.
     *
     * @param pdu the message PDU, or the datagram portion of a CDMA WDP datagram segment
     * @param address the originating address
     * @param referenceNumber distinguishes concatenated messages from the same sender
     * @param sequenceNumber the order of this segment in the message
     *          (starting at 0 for CDMA WDP datagrams and 1 for concatenated messages).
     * @param messageCount the number of segments in the message
     * @param timestamp the service center timestamp in millis
     * @param destPort the destination port for the message, or -1 for no destination port
     * @param isCdmaWapPush true if pdu is a CDMA WDP datagram segment and not an SM PDU
     *
     * @return a result code from {@link Telephony.Sms.Intents}, or
     *         {@link Activity#RESULT_OK} if the message has been broadcast
     *         to applications
     */
    protected int processMessagePart(byte[] pdu, String address, int referenceNumber,
            int sequenceNumber, int messageCount, long timestamp, int destPort,
            boolean isCdmaWapPush) {
        byte[][] pdus = null;
        Cursor cursor = null;
        try {
            // used by several query selection arguments
            String refNumber = Integer.toString(referenceNumber);
            String seqNumber = Integer.toString(sequenceNumber);

            // Check for duplicate message segment 检查有没有重复的片段，有就忽略了
            cursor = mResolver.query(mRawUri, PDU_PROJECTION,
                    "address=? AND reference_number=? AND sequence=?",
                    new String[] {address, refNumber, seqNumber}, null);

            // moveToNext() returns false if no duplicates were found
            if (cursor.moveToNext()) {
                Log.w(TAG, "Discarding duplicate message segment from address=" + address
                        + " refNumber=" + refNumber + " seqNumber=" + seqNumber);
                String oldPduString = cursor.getString(PDU_COLUMN);
                byte[] oldPdu = HexDump.hexStringToByteArray(oldPduString);
                if (!Arrays.equals(oldPdu, pdu)) {
                    Log.e(TAG, "Warning: dup message segment PDU of length " + pdu.length
                            + " is different from existing PDU of length " + oldPdu.length);
                }
                return Intents.RESULT_SMS_HANDLED;
            }
            cursor.close();

            // not a dup, query for all other segments of this concatenated message
            String where = "address=? AND reference_number=?";
            String[] whereArgs = new String[] {address, refNumber};
            cursor = mResolver.query(mRawUri, PDU_SEQUENCE_PORT_PROJECTION, where, whereArgs, null);

            int cursorCount = cursor.getCount();
            if (cursorCount != messageCount - 1) { //如果不是最后一条，就插入raw表
                // We don't have all the parts yet, store this one away
                ContentValues values = new ContentValues();
                values.put("date", timestamp);
                values.put("pdu", HexDump.toHexString(pdu));
                values.put("address", address);
                values.put("reference_number", referenceNumber);
                values.put("count", messageCount);
                values.put("sequence", sequenceNumber);
                if (destPort != -1) {
                    values.put("destination_port", destPort);
                }
                mResolver.insert(mRawUri, values);
                return Intents.RESULT_SMS_HANDLED;
            }

            // All the parts are in place, deal with them
            pdus = new byte[messageCount][];
            for (int i = 0; i &lt; cursorCount; i++) {
                cursor.moveToNext();
                int cursorSequence = cursor.getInt(SEQUENCE_COLUMN);
                // GSM sequence numbers start at 1; CDMA WDP datagram sequence numbers start at 0
                if (!isCdmaWapPush) {
                    cursorSequence--;
                }
                pdus[cursorSequence] = HexDump.hexStringToByteArray(
                        cursor.getString(PDU_COLUMN));

                // Read the destination port from the first segment (needed for CDMA WAP PDU).
                // It's not a bad idea to prefer the port from the first segment for 3GPP as well.
                if (cursorSequence == 0 && !cursor.isNull(DESTINATION_PORT_COLUMN)) {
                    destPort = cursor.getInt(DESTINATION_PORT_COLUMN);
                }
            }
            // This one isn't in the DB, so add it
            // GSM sequence numbers start at 1; CDMA WDP datagram sequence numbers start at 0
            if (isCdmaWapPush) {
                pdus[sequenceNumber] = pdu;
            } else {
                pdus[sequenceNumber - 1] = pdu;
            }

            // Remove the parts from the database
            mResolver.delete(mRawUri, where, whereArgs);
        } catch (SQLException e) {
            Log.e(TAG, "Can't access multipart SMS database", e);
            return Intents.RESULT_SMS_GENERIC_ERROR;
        } finally {
            if (cursor != null) cursor.close();
        }

        // Special handling for CDMA WDP datagrams
        if (isCdmaWapPush) {
            // Build up the data stream
            ByteArrayOutputStream output = new ByteArrayOutputStream();
            for (int i = 0; i &lt; messageCount; i++) {
                // reassemble the (WSP-)pdu
                output.write(pdus[i], 0, pdus[i].length);
            }
            byte[] datagram = output.toByteArray();

            // Dispatch the PDU to applications
            if (destPort == SmsHeader.PORT_WAP_PUSH) {
                // Handle the PUSH
                return mWapPush.dispatchWapPdu(datagram);
            } else {
                pdus = new byte[1][];
                pdus[0] = datagram;
                // The messages were sent to any other WAP port
                dispatchPortAddressedPdus(pdus, destPort);
                return Activity.RESULT_OK;
            }
        }

        // Dispatch the PDUs to applications
        if (destPort != -1) {
            if (destPort == SmsHeader.PORT_WAP_PUSH) {
                // Build up the data stream
                ByteArrayOutputStream output = new ByteArrayOutputStream();
                for (int i = 0; i &lt; messageCount; i++) {
                    SmsMessage msg = SmsMessage.createFromPdu(pdus[i], getFormat());
                    byte[] data = msg.getUserData();
                    output.write(data, 0, data.length);
                }
                // Handle the PUSH
                return mWapPush.dispatchWapPdu(output.toByteArray());
            } else {
                // The messages were sent to a port, so concoct a URI for it
                dispatchPortAddressedPdus(pdus, destPort);
            }
        } else {
            // The messages were not sent to a port
            dispatchPdus(pdus);
        }
        return Activity.RESULT_OK;
    }

    /**
     * Dispatches standard PDUs to interested applications
     *
     * @param pdus The raw PDUs making up the message
     */
    protected void dispatchPdus(byte[][] pdus) {
        Intent intent = new Intent(Intents.SMS_RECEIVED_ACTION);
        intent.putExtra("pdus", pdus);
        intent.putExtra("format", getFormat());
        dispatch(intent, RECEIVE_SMS_PERMISSION);
    }</pre>
## 参考

<a href="http://blog.csdn.net/tanghaibo001/article/details/7548727" target="_blank">Android MMS模块数据存取</a>  
<a href="http://yinger-fei.iteye.com/blog/1517613" target="_blank">android sms接收流程（ril分析）</a>  
<a href="http://minhdanh2002.blogspot.com/2012/02/raw-access-to-sms-database-on-android.html" title="Raw access to SMS/MMS database on Android phones" target="_blank">Raw access to SMS/MMS database on Android phones</a>