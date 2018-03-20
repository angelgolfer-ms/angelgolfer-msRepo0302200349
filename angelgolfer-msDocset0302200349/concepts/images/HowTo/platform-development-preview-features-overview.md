ms.TocTitle: Preview features
Title: Preview developer features on the Office 365 platform
Description: Office 365 preview functionality and APIs are not yet finalized for production code, but get an early look at some of what we're building into the platform.
ms.ContentId: 4bbbd683-c12a-449a-9215-823ce7ffd8de
ms.topic: article (how-tos)
ms.date: November 17, 2015

[!INCLUDE [Add the O365API repo styles](../includes/controls/addo365apistyles.xml)]



# Preview developer features on the Office 365 platform

_**Applies to:** Office 365_

    
We're always striving to improve and expand the Office 365 development platform. We've added Preview versions of several developer features for Office 365.

##What are Office 365 preview features?

Office 365 preview features are functionality and APIs that we've made publicly available to developers to provide an early look at what we're building, and to gather feedback about the features and how they work. Preview features are subject to change prior to finalization, possibly even changes that would break code written using them. Because of this, features and APIs marked as preview in Office 365 should not be used in production code.

While these features are currently in preview and not yet finalized for use in production code, they give you an early look at some of the functionality we're building into the platform going forward, and a chance to let us know what you think.

##Preview features for the Office 365 APIs

The following diagram of the Office 365 API development stack shows  features that are currently in preview, formatted in purple.

<svg xmlns:xlink="http://www.w3.org/1999/xlink" height="689px" width="600px">

<style type="text/css">
	.st0{fill:#737373;}
	.st1{fill:#FFFFFF;}
	.st2{font-family:'Arial';}
	.st3{font-size:11px;}
	.st4{fill:#DCD3E8;}
	.st5{fill:#68BD45;}
	.st6{fill:#C3E5B5;}
	.st7{fill:#A4A4A4;}
	.st8{fill:#00ABEC;}
	.st9{fill:#D8D8D8;}
	.st10{fill:#2273B9;}
	.st11{fill:#B7E0FF;}
	.st12{fill:#623997;}
	.st13{fill:#8EDAF7;}
	.st14{clip-path:url(#SVGID_2_);}
	.st15{clip-path:url(#SVGID_4_);fill:#68BD45;}
	.st16{clip-path:url(#SVGID_4_);fill:#FFFFFF;}
	.st17{clip-path:url(#SVGID_6_);}
	.st18{clip-path:url(#SVGID_8_);fill:#68BD45;}
	.st19{clip-path:url(#SVGID_8_);fill:#FFFFFF;}
	.st20{fill:#2372BA;}
	.st21{fill-rule:evenodd;clip-rule:evenodd;fill:#FFFFFF;}
	.st22{fill:#FFFFFF;stroke:#2273B9;stroke-miterlimit:10;}
	.st23{fill:none;stroke:#DA4026;stroke-width:2;stroke-miterlimit:10;}
	.st24{fill:none;stroke:#DA4026;stroke-width:2;stroke-miterlimit:10;stroke-dasharray:11.9529,11.9529;}
	.st25{fill:none;stroke:#DA4026;stroke-width:2;stroke-miterlimit:10;stroke-dasharray:12.1257,12.1257;}
	.st26{fill:#505050;}
	.st27{fill:#DA4026;}
	.st28{fill:none;stroke:#505050;stroke-width:4;stroke-miterlimit:10;}
	.st29{font-size:21px;}
	.st30{fill:#7F1D1D;stroke:#2273B9;stroke-width:4;stroke-miterlimit:10;}
	.st31{fill:#7F1D1D;stroke:#A4A4A4;stroke-width:4;stroke-miterlimit:10;}
	.st32{font-size:14px;}
	.st33{font-family:'Arial';}
	.st34{font-size:9px;}
	.st35{fill:#231F20;}
	.st36{fill:#F25022;}
	.st37{fill:#7FBA00;}
	.st38{fill:#00A4EF;}
	.st39{fill:#FFB900;}
	.st40{fill:none;stroke:#682A7A;stroke-width:2;stroke-miterlimit:10;}
	.st41{fill:none;stroke:#682A7A;stroke-width:2;stroke-miterlimit:10;stroke-dasharray:11.9529,11.9529;}
	.st42{fill:none;stroke:#682A7A;stroke-width:2;stroke-miterlimit:10;stroke-dasharray:13.1178,13.1178;}
	.st43{fill:none;stroke:#2273B9;stroke-width:4;stroke-miterlimit:10;}
	.st44{clip-path:url(#SVGID_10_);}
	.st45{clip-path:url(#SVGID_12_);fill:#FFFFFF;}
	.st46{clip-path:url(#SVGID_12_);fill:#00ABEC;}
	.st47{clip-path:url(#SVGID_12_);fill:#FFFFFF;stroke:#00ABEC;stroke-miterlimit:10;}
	.st48{clip-path:url(#SVGID_14_);fill:#FFFFFF;}
	.st49{clip-path:url(#SVGID_14_);}
	.st50{clip-path:url(#SVGID_16_);fill:#2273B9;}
	.st51{clip-path:url(#SVGID_18_);}
	.st52{clip-path:url(#SVGID_20_);fill:#FFFFFF;}
	.st53{clip-path:url(#SVGID_20_);fill:#00ABEC;}
	.st54{clip-path:url(#SVGID_22_);}
	.st55{clip-path:url(#SVGID_24_);fill:#FFFFFF;}
	.st56{clip-path:url(#SVGID_24_);fill:#00ABEC;}
	.st57{clip-path:url(#SVGID_26_);}
	.st58{clip-path:url(#SVGID_28_);fill:#FFFFFF;}
	.st59{clip-path:url(#SVGID_28_);fill:#2273B9;}
	.st60{clip-path:url(#SVGID_30_);fill:#FFFFFF;}
	.st61{clip-path:url(#SVGID_30_);fill:#2273B9;}
	.st62{clip-path:url(#SVGID_32_);fill:#FFFFFF;}
	.st63{clip-path:url(#SVGID_32_);fill:#2273B9;}
	.st64{fill:#FFFFFF;stroke:#2273B9;stroke-width:2;stroke-miterlimit:10;}
	.st65{font-family:'Arial';}
	.st66{font-size:12px;}
	.st67{fill:none;stroke:#2273B9;stroke-width:2;stroke-miterlimit:10;}
	.st68{clip-path:url(#SVGID_34_);}
	.st69{clip-path:url(#SVGID_36_);fill:#FFFFFF;}
	.st70{clip-path:url(#SVGID_36_);fill:#2273B9;}
	.st71{fill-rule:evenodd;clip-rule:evenodd;fill:#00ABEC;stroke:#FFFFFF;stroke-width:1.5;stroke-miterlimit:10;}
	.st72{fill:none;stroke:#FFFFFF;stroke-width:1.5;stroke-miterlimit:10;}
	.st73{clip-path:url(#SVGID_38_);fill:#FFFFFF;}
	.st74{fill:none;}
	.st75{font-family:'Arial';}
	.st76{fill-rule:evenodd;clip-rule:evenodd;fill:#68BD45;}
</style>
<g id="Gray_boxes">
	<rect x="5" y="11" class="st0" width="101" height="132"/>
	<rect x="5" y="154" class="st0" width="101" height="112"/>
	<rect x="5" y="279" class="st0" width="101" height="161"/>
	<rect x="5" y="450" class="st0" width="101" height="226"/>
	<text transform="matrix(1 0 0 1 19 207.6622)"><tspan x="0" y="0" class="st1 st2 st3">Development  </tspan><tspan x="0" y="13.2" class="st1 st2 st3">Environment</tspan></text>
	<text transform="matrix(1 0 0 1 19 81.1622)" class="st1 st2 st3">Solution</text>
	<text transform="matrix(1 0 0 1 19 359.6149)" class="st1 st2 st3">Authentication</text>
	<text transform="matrix(1 0 0 1 19 559.1622)" class="st1 st2 st3">Data</text>
</g>
<g id="ENCLOSURES">
</g>
<g id="LINES__x2F__ARROWS">
	<rect x="115" y="311" class="st4" width="478" height="129"/>
	<rect x="115" y="11" class="st5" width="478" height="39"/>
	<rect x="115" y="48" class="st6" width="478.2" height="95.2"/>
	<rect x="123" y="57" class="st7" width="463" height="33"/>
	<rect x="123" y="98" class="st8" width="230" height="33.8"/>
	<rect x="357" y="98" class="st7" width="228.7" height="33.8"/>
	<rect x="115" y="154" class="st9" width="478.2" height="113"/>
	<rect x="123" y="168" class="st7" width="111" height="34"/>
	<rect x="241" y="168" class="st7" width="112" height="34"/>
	<rect x="357" y="168" class="st7" width="111" height="34"/>
	<rect x="473" y="168" class="st7" width="113" height="34"/>
	<rect x="123" y="210" class="st10" width="111" height="33"/>
	<rect x="241" y="210" class="st10" width="112" height="33"/>
	<rect x="357" y="210" class="st10" width="111" height="33"/>
	<rect x="123" y="361" class="st8" width="224.8" height="38"/>
	<rect x="354.1" y="361" class="st11" width="231.9" height="38"/>
	<rect x="123.2" y="322" class="st12" width="462.8" height="28"/>
	<rect x="123" y="407" class="st7" width="463" height="20"/>
	<rect x="123" y="505" class="st10" width="463" height="24"/>
	<rect x="123" y="539" class="st10" width="39" height="109.8"/>
	<rect x="255" y="539" class="st10" width="39" height="109.8"/>
	<rect x="429" y="539" class="st8" width="39" height="109.8"/>
	<rect x="162" y="539" class="st11" width="87" height="109.8"/>
	<rect x="294" y="539" class="st11" width="128" height="109.8"/>
	<rect x="468" y="539" class="st13" width="52" height="109.8"/>
	<rect x="526" y="539" class="st12" width="60" height="121.5"/>
	<rect x="123" y="655" class="st12" width="463" height="10"/>
	<text transform="matrix(1 0 0 1 288.1081 70.4953)"><tspan x="0" y="0" class="st2 st3">Your choice of technology</tspan><tspan x="-20.6" y="13.2" class="st2 st3">(.NET, JavaScript, HTML, Ruby, etc.)</tspan></text>
	<text transform="matrix(1 0 0 1 437.4897 111.162)"><tspan x="0" y="0" class="st2 st3">Other hosting</tspan><tspan x="-3.6" y="13.2" class="st2 st3">(IIS, LAMP, etc.)</tspan></text>
	<text transform="matrix(1 0 0 1 162.6362 188.4955)" class="st2 st3">XCode</text>
	<text transform="matrix(1 0 0 1 272.5954 182.162)"><tspan x="0" y="0" class="st2 st3">Eclipse or </tspan><tspan x="-13.7" y="13.2" class="st2 st3">Android Studio</tspan></text>
	<text transform="matrix(1 0 0 1 379.4771 188.4953)" class="st2 st3">Visual Studio</text>
	<text transform="matrix(1 0 0 1 517.7487 188.4955)" class="st2 st3">REST</text>
	<text transform="matrix(1 0 0 1 170.2235 222.8288)"><tspan x="0" y="0" class="st1 st2 st3">iOS </tspan><tspan x="-27.8" y="13.2" class="st1 st2 st3">Office 365 SDK</tspan></text>
	<text transform="matrix(1 0 0 1 276.0621 222.8288)"><tspan x="0" y="0" class="st1 st2 st3">Android </tspan><tspan x="-16.6" y="13.2" class="st1 st2 st3">Office 365 SDK</tspan></text>
	<text transform="matrix(1 0 0 1 381.1005 222.829)"><tspan x="0" y="0" class="st1 st2 st3">Visual Studio </tspan><tspan x="-4.7" y="13.2" class="st1 st2 st3">Office 365 SDK</tspan></text>
	<g>
		<path class="st5" d="M300.5,42.3c-1.4,0-2.5-0.6-2.9-1.5c-0.3-0.7-0.2-1.5,0.4-2.1c0.3-0.3,0.8-0.7,1.3-1.2
			c0.4-0.4,0.8-0.8,1.2-1.1V20.9c0-1.7,1.2-3,2.9-3h26.9c1.7,0,3,1.3,3,3v15.6c0.3,0.3,0.8,0.7,1.2,1.1c0.5,0.4,0.9,0.8,1.2,1.1
			c0.6,0.6,0.8,1.4,0.5,2.1c-0.4,1-1.5,1.5-3,1.5H300.5z"/>
		<path class="st1" d="M334.7,39.5c-0.7-0.7-2.1-1.9-2.7-2.6V20.9c0-1-0.7-1.8-1.8-1.8h-26.9c-1,0-1.7,0.7-1.7,1.8V37
			c-0.7,0.7-2.1,1.9-2.8,2.6c-0.6,0.7,0,1.6,1.7,1.6h32.6C334.7,41.2,335.4,40.2,334.7,39.5z M319.9,40h-6.2c-0.2,0-0.3-0.2-0.2-0.3
			l1-1.4c0-0.1,0.1-0.1,0.2-0.1h4.2c0.1,0,0.1,0,0.2,0.1l1,1.4C320.1,39.8,320,40,319.9,40z M330.2,36.4h-26.8V20.9h26.8V36.4z"/>
	</g>
	<g>
		<g>
			<defs>
				<rect id="SVGID_1_" x="233.5" y="13.3" width="31.7" height="33.6"/>
			</defs>
			<clipPath id="SVGID_2_">
				<use xlink:href="#SVGID_1_"  style="overflow:visible;"/>
			</clipPath>
			<g class="st14">
				<defs>
					<rect id="SVGID_3_" x="233.5" y="13.3" width="31.7" height="33.6"/>
				</defs>
				<clipPath id="SVGID_4_">
					<use xlink:href="#SVGID_3_"  style="overflow:visible;"/>
				</clipPath>
				<path class="st15" d="M244.2,44.3c-1.3,0-2.4-1.2-2.4-2.6V18.5c0-1.4,1.1-2.6,2.4-2.6h10.7c1.3,0,2.4,1.2,2.4,2.6v23.3
					c0,1.4-1.1,2.6-2.4,2.6H244.2z"/>
				<path class="st16" d="M254.9,16.9h-10.7c-0.8,0-1.5,0.7-1.5,1.6v23.3c0,0.9,0.7,1.6,1.5,1.6h10.7c0.8,0,1.5-0.7,1.5-1.6V18.5
					C256.4,17.6,255.7,16.9,254.9,16.9 M250.5,41.7h-1.9c-0.4,0-0.7-0.3-0.7-0.8s0.3-0.8,0.7-0.8h1.9c0.4,0,0.7,0.3,0.7,0.8
					S250.9,41.7,250.5,41.7 M254.9,38.6h-10.7V20h10.7V38.6z"/>
			</g>
		</g>
	</g>
	<g>
		<g>
			<defs>
				<rect id="SVGID_5_" x="259.9" y="10.9" width="37.5" height="37.5"/>
			</defs>
			<clipPath id="SVGID_6_">
				<use xlink:href="#SVGID_5_"  style="overflow:visible;"/>
			</clipPath>
			<g class="st17">
				<defs>
					<rect id="SVGID_7_" x="259.9" y="10.9" width="37.5" height="37.5"/>
				</defs>
				<clipPath id="SVGID_8_">
					<use xlink:href="#SVGID_7_"  style="overflow:visible;"/>
				</clipPath>
				<path class="st18" d="M265.1,42.6c-1.6,0-2.9-1.3-2.9-2.8V20c0-1.5,1.3-2.8,2.9-2.8h27.2c1.5,0,2.8,1.3,2.8,2.8v19.8
					c0,1.5-1.3,2.8-2.8,2.8H265.1z"/>
				<path class="st19" d="M292.8,22.4v17.4c0,0.3,0.3,0.8,0-1l-28.3-0.1c-0.3,1.8,0,1.4,0,1.1V22.4H292.8z M292.3,18.4h-27.2
					c-0.9,0-1.7,0.8-1.7,1.7v19.8c0,0.9,0.8,1.6,1.7,1.6h27.2c0.9,0,1.6-0.7,1.6-1.7V20C293.9,19.1,293.2,18.4,292.3,18.4"/>
				<rect x="291.6" y="19.5" class="st19" width="1.2" height="1.2"/>
				<rect x="289.3" y="19.5" class="st19" width="1.2" height="1.2"/>
				<rect x="287" y="19.5" class="st19" width="1.2" height="1.2"/>
			</g>
		</g>
	</g>
	<g>
		<path class="st10" d="M289.1,549.8h-10.8v-7.4h-2.3l-17.7,3.1V572l17,3h3v-6.9h10.8c1,0,1.9-0.8,1.9-1.9v-14.6
			C291,550.6,290.1,549.8,289.1,549.8z"/>
		<g>
			<path class="st1" d="M289.1,550.9h-11.8v-7.6l-17.9,3.2v24.7l17.9,3.1v-7.2h11.8c0.4,0,0.8-0.4,0.8-0.8v-14.6
				C289.9,551.2,289.6,550.9,289.1,550.9z M288.9,566.1h-11.6v-9.3l3.6,3.5c0.1,0.1,0.3,0.2,0.5,0.2c0.2,0,0.4-0.1,0.5-0.2l6.9-6.4
				V566.1z M288.9,552.5l-7.4,6.9l-4.2-4v-3.6h11.6V552.5z"/>
			<path class="st10" d="M268,562.4c-3.2-0.1-3.1-7,0.1-7.1C271.2,555.1,271.3,562.5,268,562.4 M268.1,553.1
				c-5.8,0.4-6,11.1-0.1,11.4C274.2,564.9,274.4,552.7,268.1,553.1"/>
		</g>
	</g>
	<g>
		<g>
			<path class="st10" d="M154.7,595.3c-0.2-2.2-1.6-3.7-3-4.3c-0.4-0.2-0.8-0.3-1.1-0.4l0-0.1c-0.2-2.1-1.6-4.9-4.7-6.1
				c-0.9-0.4-1.8-0.5-2.8-0.5c-2.3,0-4.4,1.1-5.8,3c-0.5-0.2-1.2-0.4-2-0.4c-0.9,0-1.8,0.2-2.7,0.7c-1.9,1-3.1,3-3.2,5.1
				c-1.6,0.5-3.6,1.8-3.6,4.9c0,2.7,2.3,5,4.9,5h3.5c0.9,0.8,2.1,1.3,3.6,1.3h16c2.5,0,3.8-2.1,3.8-4.2
				C157.5,597,155.9,595.8,154.7,595.3z"/>
			<path class="st1" d="M153.7,596.1c0,0,2.8,0.3,2.8,3.3c0,1.5-0.8,3.2-2.8,3.2c0,0-15,0-16,0c-3.1,0-4.2-2.1-4.2-4.2
				c0-3.6,4-3.7,4-3.7s0.3-4,3.8-4.8c3.1-0.7,4.9,0.9,5.7,2.2c0,0,1.9-1.1,4.1-0.1C152.5,592.5,153.8,593.9,153.7,596.1z"/>
			<path class="st1" d="M132.5,598.6c0-4,4.3-4.6,4.3-4.6s0.5-3.9,4.4-4.9c3-0.8,5.3,0.6,6.2,2.1c0,0,0.6-0.5,2.1-0.4
				c-0.1-1.3-1.1-4.1-4.1-5.3c-3.4-1.3-6.4,0.3-7.8,2.8c0,0-2.1-1.4-4.6-0.1c-1.8,0.9-2.9,3-2.6,5.1c0,0-3.6,0.3-3.6,4.1
				c0,2.1,1.9,4,3.9,4h2.7C132.7,600.4,132.5,599.4,132.5,598.6z"/>
		</g>
	</g>
	<g>
		<path class="st20" d="M155.1,554c-1-1.7-2.4-3.1-4-4c-0.5-2.3-2.5-4-4.9-4.1v-3.3l-19.9,3.5v26.4l19.9,3.5v-3.4
			c2.4-0.1,4.4-1.8,4.9-4.1c1.7-0.9,3.1-2.3,4-4c2.4-0.5,4.2-2.7,4.2-5.2C159.3,556.6,157.5,554.5,155.1,554z M149.5,562.1
			c-0.2,0.2-0.4,0.5-0.7,0.7c-0.8-0.5-1.7-0.8-2.6-0.9v-5.5c0.9-0.1,1.9-0.4,2.6-0.9c0.3,0.2,0.5,0.4,0.7,0.7
			c-0.6,0.9-0.9,1.9-0.9,2.9C148.6,560.2,148.9,561.2,149.5,562.1z"/>
		<path class="st21" d="M145.8,570.9c-2,0-3.7-1.6-3.8-3.6c-2-0.9-3.6-2.5-4.5-4.4c-2-0.1-3.6-1.7-3.6-3.7c0-2,1.6-3.7,3.6-3.7
			c0.9-2,2.5-3.5,4.5-4.4c0.1-2,1.7-3.6,3.8-3.6c2,0,3.7,1.6,3.8,3.6c2,0.9,3.6,2.5,4.5,4.4c2,0.1,3.6,1.7,3.6,3.7
			c0,2-1.6,3.7-3.6,3.7c-0.9,2-2.5,3.5-4.5,4.4C149.5,569.3,147.9,570.9,145.8,570.9z M140.2,561.9c0.6,1.2,1.6,2.2,2.8,2.8
			c0.7-0.8,1.7-1.3,2.8-1.3c1.1,0,2.1,0.5,2.8,1.3c1.2-0.6,2.2-1.6,2.8-2.8c-0.8-0.7-1.3-1.7-1.3-2.8c0-1.1,0.5-2.1,1.3-2.8
			c-0.6-1.2-1.6-2.2-2.8-2.8c-0.7,0.8-1.7,1.3-2.8,1.3c-1.1,0-2.1-0.5-2.8-1.3c-1.2,0.6-2.2,1.6-2.8,2.8c0.8,0.7,1.3,1.7,1.3,2.8
			C141.5,560.2,141,561.2,140.2,561.9z"/>
		<path class="st20" d="M144.9,571.3c0.3,0.1,0.6,0.1,0.9,0.1c2.2,0,4-1.7,4.3-3.8c1.9-0.9,3.4-2.4,4.3-4.3c2.1-0.2,3.8-2,3.8-4.2
			c0-2.2-1.7-4-3.8-4.2c-0.9-1.8-2.5-3.4-4.3-4.3c-0.2-2.1-2.1-3.8-4.3-3.8c-0.3,0-0.6,0-0.9,0.1 M144.9,555.3
			c0.3,0.1,0.6,0.1,0.9,0.1c1.1,0,2.1-0.4,2.9-1.1c0.8,0.5,1.5,1.2,2,2c-0.7,0.8-1.1,1.8-1.1,2.9c0,1.1,0.4,2.1,1.1,2.9
			c-0.5,0.8-1.2,1.5-2,2c-0.8-0.7-1.8-1.1-2.9-1.1c-0.3,0-0.6,0-0.9,0.1V555.3z M153.9,562.4c-0.1,0-0.1,0-0.2,0
			c-0.9,2.1-2.6,3.8-4.7,4.6c0,0.1,0,0.1,0,0.2c0,1.8-1.4,3.2-3.2,3.2c-0.3,0-0.6,0-0.9-0.1v-6.2c0.3-0.1,0.6-0.1,0.9-0.1
			c1.1,0,2.1,0.6,2.7,1.4c1.6-0.7,2.9-2,3.6-3.6c-0.8-0.6-1.4-1.6-1.4-2.6s0.6-2.1,1.4-2.6c-0.7-1.6-2-2.9-3.6-3.6
			c-0.6,0.8-1.6,1.4-2.7,1.4c-0.3,0-0.6-0.1-0.9-0.1V548c0.3-0.1,0.6-0.1,0.9-0.1c1.8,0,3.2,1.4,3.2,3.2c0,0.1,0,0.1,0,0.2
			c2.1,0.9,3.8,2.5,4.7,4.6c0.1,0,0.1,0,0.2,0c1.8,0,3.2,1.4,3.2,3.2C157.2,560.9,155.7,562.4,153.9,562.4z"/>
		<path class="st22" d="M145.1,543.7l-17.8,3.1v24.6l17.8,3.1V543.7z"/>
		<path class="st10" d="M136.4,552.9c-1.5,0.1-2.9,0.9-3.3,2.4c-0.4,1.5,0.1,3,1.4,3.9c0.8,0.6,3.1,1.4,2.3,2.8
			c-0.3,0.6-1.1,0.6-1.7,0.5c-0.8-0.1-1.5-0.6-2.1-1.2c0,0.4,0,0.9,0,1.3c0,0.3,0,0.6,0,0.8c0,0.3,0.1,0.3,0.4,0.5
			c1.8,1,4.9,0.8,5.7-1.4c0.4-1,0.3-2.3-0.3-3.2c-0.6-0.9-1.6-1.4-2.5-1.9c-0.4-0.2-0.9-0.5-1-1c-0.2-0.5-0.1-1,0.3-1.3
			c0.9-0.8,2.5-0.2,3.3,0.4c0-0.6,0-1.2,0-1.9c0-0.1,0-0.3,0-0.4c0-0.2-0.1-0.1-0.3-0.2C137.8,552.9,137.1,552.8,136.4,552.9"/>
	</g>
	<g>
		<g>
			<polyline class="st23" points="593.2,486.3 593.2,480.3 587.2,480.3 			"/>
			<line class="st24" x1="575.2" y1="480.3" x2="127" y2="480.3"/>
			<polyline class="st23" points="121,480.3 115,480.3 115,486.3 			"/>
			<line class="st25" x1="115" y1="498.4" x2="115" y2="662.1"/>
			<polyline class="st23" points="115,668.2 115,674.2 121,674.2 			"/>
			<line class="st24" x1="133" y1="674.2" x2="581.2" y2="674.2"/>
			<polyline class="st23" points="587.2,674.2 593.2,674.2 593.2,668.2 			"/>
			<line class="st25" x1="593.2" y1="656" x2="593.2" y2="492.3"/>
		</g>
	</g>
	<g>
		<g>
			<path class="st1" d="M138.9,494.6c-6.2,0-11.2-5.3-11.2-11.9c0-6.4,4.8-11.6,10.8-11.8c1.9-2.3,4.5-3.6,7.4-3.7
				c1.2-6.1,6.3-10.6,12.4-10.6c4,0,7.7,2,10.1,5.4c1.1-0.4,2.3-0.5,3.5-0.5c6.8,0,12.3,5.8,12.3,13c0,0.1,0,0.1,0,0.2
				c2.8,2,4.5,5.4,4.5,9c0,5-3.2,9.4-7.9,10.7l-0.1,0l-1.5,0.3H138.9z"/>
			<path class="st26" d="M182,475.6c0-0.4,0.1-0.8,0.1-1.2c0-6.1-4.6-11-10.3-11c-1.5,0-3,0.3-4.3,1c-1.9-3.6-5.4-5.8-9.2-5.8
				c-5.7,0-10.3,4.7-10.7,10.7c-0.4-0.1-0.9-0.1-1.3-0.1c-2.7,0-5.2,1.4-6.8,3.8c-0.2,0-0.4,0-0.6,0c-5.1,0-9.2,4.4-9.2,9.8
				c0,5.4,4.1,9.9,9.2,9.9H179l1.3-0.3c3.8-1,6.4-4.6,6.4-8.7C186.6,480.2,184.9,477.1,182,475.6 M179.8,490.3l-1,0.2h-39.9
				c-4,0-7.2-3.5-7.2-7.9c0-4.3,3.2-7.8,7.2-7.8c0.2,0,0.3,0,0.5,0l1.2,0.1l0.6-1c1.2-1.8,3.1-2.9,5.1-2.9c0.3,0,0.7,0,1,0.1
				l2.2,0.4l0.1-2.3c0.3-4.9,4.1-8.8,8.7-8.8c3.1,0,5.9,1.8,7.5,4.8l0.9,1.7l1.8-0.9c1.1-0.5,2.2-0.8,3.4-0.8c4.6,0,8.3,4,8.3,9
				c0,0.3,0,0.7-0.1,1l-0.1,1.3l1.2,0.6c2.2,1.2,3.6,3.6,3.6,6.2C184.6,486.8,182.7,489.5,179.8,490.3"/>
			<polygon class="st1" points="183.1,451.6 192.7,454.1 192.7,479 183.1,481.4 166.7,475.7 166.7,457.2 			"/>
			<polygon class="st27" points="190.7,477.4 190.7,455.7 183.2,453.7 168.7,458.7 168.7,458.7 168.7,474.4 173.7,472.5 
				173.7,459.7 183.7,457.5 183.7,476.3 168.7,474.4 183.2,479.3 			"/>
		</g>
	</g>
	<g>
		<g>
			<line class="st28" x1="354.1" y1="300.4" x2="354.1" y2="275.1"/>
			<g>
				<polygon class="st26" points="359.3,298.9 354.1,307.9 348.9,298.9 				"/>
			</g>
			<g>
				<polygon class="st26" points="359.3,276.7 354.1,267.7 348.9,276.7 				"/>
			</g>
		</g>
	</g>
	<text transform="matrix(1 0 0 1 132.1909 33.6622)" class="st1 st2 st3">Your app</text>
	<text transform="matrix(1 0 0 1 340.1709 39.9591)" class="st1 st2 st29">...</text>
	<line class="st30" x1="178.6" y1="240.9" x2="178.6" y2="256.7"/>
	<line class="st30" x1="296" y1="241.4" x2="296" y2="257.2"/>
	<line class="st30" x1="413" y1="240.4" x2="413" y2="256.2"/>
	<line class="st31" x1="529.6" y1="200.8" x2="529.6" y2="216.5"/>
	<text transform="matrix(1 0 0 1 197.9624 120.1622)" class="st1 st2 st32">Microsoft Azure</text>
	<text transform="matrix(1 0 0 1 167.2066 378.055)"><tspan x="0" y="0" class="st1 st2 st3">Work or school ID (Azure AD) </tspan><tspan x="11.1" y="10.8" class="st1 st33 st34">user@domain.onmicrosoft.com</tspan></text>
	<text transform="matrix(1 0 0 1 419.2991 378.305)"><tspan x="0" y="0" class="st35 st2 st3">Personal (Microsoft ID) </tspan><tspan x="-20.5" y="10.8" class="st35 st33 st34">user@live.com, user@hotmail.com, etc.</tspan></text>
	<text transform="matrix(1 0 0 1 329.192 519.9997)" class="st1 st2 st3">REST APIs</text>
	<text transform="matrix(1 0 0 1 275.085 420.805)" class="st35 st2 st3">OAuth 2.0 and Open ID Connect 1.0</text>
	<g>
		<rect x="359.2" y="366.3" class="st36" width="13.9" height="13.9"/>
		<rect x="374.7" y="366.3" class="st37" width="13.9" height="13.9"/>
		<rect x="359.2" y="382.2" class="st38" width="13.9" height="13.9"/>
		<rect x="374.7" y="382.2" class="st39" width="13.9" height="13.9"/>
	</g>
	<g>
		<g>
			<line class="st28" x1="353.1" y1="472.8" x2="353.1" y2="447.5"/>
			<g>
				<polygon class="st26" points="358.3,471.3 353.1,480.3 347.9,471.3 				"/>
			</g>
			<g>
				<polygon class="st26" points="358.3,449 353.1,440 347.9,449 				"/>
			</g>
		</g>
	</g>
	<g>
		<g>
			<polyline class="st40" points="593,316 593,310 587,310 			"/>
			<line class="st41" x1="575" y1="310" x2="126.8" y2="310"/>
			<polyline class="st40" points="120.8,310 114.8,310 114.8,316 			"/>
			<line class="st42" x1="114.8" y1="329.1" x2="114.8" y2="427.5"/>
			<polyline class="st40" points="114.8,434.1 114.8,440.1 120.8,440.1 			"/>
			<line class="st41" x1="132.8" y1="440.1" x2="581" y2="440.1"/>
			<polyline class="st40" points="587,440.1 593,440.1 593,434.1 			"/>
			<line class="st42" x1="593" y1="420.9" x2="593" y2="322.6"/>
		</g>
	</g>
	<path class="st1" d="M140.9,318.5c-6.2,0-11.2-5.3-11.2-11.9c0-6.4,4.8-11.6,10.8-11.8c1.9-2.3,4.5-3.6,7.4-3.7
		c1.2-6.1,6.3-10.6,12.4-10.6c4,0,7.7,2,10.1,5.4c1.1-0.4,2.3-0.5,3.5-0.5c6.8,0,12.3,5.8,12.3,13c0,0.1,0,0.1,0,0.2
		c2.8,2,4.5,5.4,4.5,9c0,5-3.2,9.4-7.9,10.7l-0.1,0l-1.5,0.3H140.9z"/>
	<path class="st26" d="M184,299.5c0-0.4,0.1-0.8,0.1-1.2c0-6.1-4.6-11-10.3-11c-1.5,0-3,0.3-4.3,1c-1.9-3.6-5.4-5.8-9.2-5.8
		c-5.7,0-10.3,4.7-10.7,10.7c-0.4-0.1-0.9-0.1-1.3-0.1c-2.7,0-5.2,1.4-6.8,3.8c-0.2,0-0.4,0-0.6,0c-5.1,0-9.2,4.4-9.2,9.8
		c0,5.4,4.1,9.9,9.2,9.9H181l1.3-0.3c3.8-1,6.4-4.6,6.4-8.7C188.6,304.1,186.9,301.1,184,299.5 M181.8,314.3l-1,0.2h-39.9
		c-4,0-7.2-3.5-7.2-7.9c0-4.3,3.2-7.8,7.2-7.8c0.2,0,0.3,0,0.5,0l1.2,0.1l0.6-1c1.2-1.8,3.1-2.9,5.1-2.9c0.3,0,0.7,0,1,0.1l2.2,0.4
		l0.1-2.3c0.3-4.9,4.1-8.8,8.7-8.8c3.1,0,5.9,1.8,7.5,4.8l0.9,1.7l1.8-0.9c1.1-0.5,2.2-0.8,3.4-0.8c4.6,0,8.3,4,8.3,9
		c0,0.3,0,0.7-0.1,1l-0.1,1.3l1.2,0.6c2.2,1.2,3.6,3.6,3.6,6.2C186.6,310.7,184.7,313.5,181.8,314.3"/>
	<g>
		<rect x="168.8" y="279.6" class="st1" width="25" height="25"/>
		<rect x="169.8" y="280.9" class="st36" width="10.6" height="10.6"/>
		<rect x="181.6" y="280.9" class="st37" width="10.6" height="10.6"/>
		<rect x="169.8" y="293" class="st38" width="10.6" height="10.6"/>
		<rect x="181.6" y="293" class="st39" width="10.6" height="10.6"/>
	</g>
	<line class="st43" x1="354" y1="492.7" x2="354" y2="508.5"/>
	<text transform="matrix(1 0 0 1 541.6622 588.0411)"><tspan x="0" y="0" class="st1 st2 st3">Office </tspan><tspan x="-0.5" y="13.2" class="st1 st2 st3">Graph </tspan><tspan x="-4.3" y="26.4" class="st1 st2 st3">insights</tspan></text>
	<g>
		<g>
			<defs>
				<rect id="SVGID_9_" x="431.6" y="542.4" width="34.1" height="34.1"/>
			</defs>
			<clipPath id="SVGID_10_">
				<use xlink:href="#SVGID_9_"  style="overflow:visible;"/>
			</clipPath>
			<g class="st44">
				<defs>
					<rect id="SVGID_11_" x="431.6" y="542.4" width="34.1" height="34.1"/>
				</defs>
				<clipPath id="SVGID_12_">
					<use xlink:href="#SVGID_11_"  style="overflow:visible;"/>
				</clipPath>
				<path class="st45" d="M436.5,572.8c-0.9,0-1.6-0.4-2-1c-0.4-0.7-0.4-1.5,0.1-2.4l12.6-22.1c0.4-0.8,1.1-1.2,1.9-1.2
					c0.8,0,1.5,0.4,1.9,1.2l12.6,22.1c0.4,0.8,0.5,1.7,0.1,2.4c-0.4,0.7-1.1,1.1-2,1.1H436.5z"/>
				<path class="st46" d="M436.5,571.8c-1.1,0-1.5-0.9-1-1.8l12.6-22.1c0.5-0.9,1.4-0.9,2,0l12.6,22.1c0.5,0.9,0.1,1.8-1,1.8H436.5z
					"/>
				<path class="st45" d="M450.1,559.1c0.3-0.1,0.7-0.3,0.9-0.5l2.5,5c-0.3,0.1-0.6,0.3-0.9,0.5L450.1,559.1z"/>
				<path class="st45" d="M451.5,566h-4.8c0,0.2,0,0.3,0,0.5c0,0.2,0,0.3,0,0.5h4.8c0-0.2,0-0.3,0-0.5
					C451.4,566.3,451.5,566.2,451.5,566"/>
				<path class="st45" d="M445.6,564.1c-0.3-0.2-0.6-0.4-1-0.5l2.6-4.9c0.3,0.2,0.6,0.4,0.9,0.5L445.6,564.1z"/>
				<path class="st47" d="M449.1,559c-1.5,0-2.7-1.2-2.7-2.7c0-1.5,1.2-2.7,2.7-2.7c1.5,0,2.7,1.2,2.7,2.7
					C451.8,557.7,450.6,559,449.1,559"/>
				<path class="st46" d="M449.1,553.9c1.3,0,2.3,1,2.3,2.3c0,1.3-1,2.3-2.3,2.3c-1.3,0-2.3-1-2.3-2.3
					C446.8,554.9,447.8,553.9,449.1,553.9 M449.1,553.1c-1.7,0-3.1,1.4-3.1,3.1c0,1.7,1.4,3.1,3.1,3.1c1.7,0,3.1-1.4,3.1-3.1
					C452.2,554.5,450.8,553.1,449.1,553.1"/>
				<path class="st45" d="M454.5,569.3c-1.5,0-2.7-1.2-2.7-2.7c0-1.5,1.2-2.7,2.7-2.7s2.7,1.2,2.7,2.7S456,569.3,454.5,569.3"/>
				<path class="st46" d="M454.5,564.2c1.3,0,2.3,1,2.3,2.3c0,1.3-1,2.3-2.3,2.3s-2.3-1-2.3-2.3
					C452.2,565.3,453.2,564.2,454.5,564.2 M454.5,563.4c-1.7,0-3.1,1.4-3.1,3.1c0,1.7,1.4,3.1,3.1,3.1s3.1-1.4,3.1-3.1
					C457.6,564.8,456.2,563.4,454.5,563.4"/>
				<path class="st45" d="M443.7,569.3c-1.5,0-2.7-1.2-2.7-2.7c0-1.5,1.2-2.7,2.7-2.7s2.7,1.2,2.7,2.7S445.2,569.3,443.7,569.3"/>
				<path class="st46" d="M443.7,564.2c1.3,0,2.3,1,2.3,2.3c0,1.3-1,2.3-2.3,2.3s-2.3-1-2.3-2.3
					C441.4,565.3,442.4,564.2,443.7,564.2 M443.7,563.4c-1.7,0-3.1,1.4-3.1,3.1c0,1.7,1.4,3.1,3.1,3.1s3.1-1.4,3.1-3.1
					C446.9,564.8,445.4,563.4,443.7,563.4"/>
			</g>
		</g>
	</g>
	<g>
		<g>
			<defs>
				<rect id="SVGID_13_" x="361.7" y="536.2" width="59" height="59"/>
			</defs>
			<clipPath id="SVGID_14_">
				<use xlink:href="#SVGID_13_"  style="overflow:visible;"/>
			</clipPath>
			<rect x="367.1" y="548" class="st48" width="48.1" height="35.4"/>
			<g class="st49">
				<defs>
					<rect id="SVGID_15_" x="361.7" y="536.2" width="59" height="59"/>
				</defs>
				<clipPath id="SVGID_16_">
					<use xlink:href="#SVGID_15_"  style="overflow:visible;"/>
				</clipPath>
				<path class="st50" d="M391.9,569.4c-0.3-1.4-0.7-2.1-1.8-2.6c-1.1-0.6-1.6-1-2-1c-0.2,0-0.3,0.1-0.4,0.1
					c-0.3,0.3-0.5,0.4-0.8,0.6c-0.1,0-0.1,0.1-0.1,0.1c-0.3,0.2-0.6,0.3-0.9,0.4c-0.6,0.2-1.1,0.3-1.8,0.3c-0.6,0-1.2-0.1-1.8-0.3
					c-0.3-0.1-0.6-0.3-0.9-0.4c-0.4-0.2-0.7-0.4-1-0.7c-0.1-0.1-0.3-0.1-0.4-0.1c-0.4,0-0.8,0.3-2,1c-1.1,0.6-1.4,1.3-1.8,2.6
					c-0.3,1.2-0.6,4.5-0.7,5.9h17C392.5,573.9,392.2,570.6,391.9,569.4"/>
				<path class="st50" d="M384.1,565.4c-2.3,0-4.2-2.1-4.2-4.6s1.9-4.6,4.2-4.6c2.3,0,4.2,2.1,4.2,4.6S386.4,565.4,384.1,565.4"/>
				<path class="st50" d="M368.9,581.6h44.5v-31.8h-44.5V581.6z M411.6,579.8h-40.8v-28.1h40.8V579.8z"/>
				<rect x="396.2" y="559.8" class="st50" width="11.8" height="1.8"/>
				<rect x="396.2" y="565.3" class="st50" width="11.8" height="1.8"/>
				<rect x="396.2" y="570.7" class="st50" width="11.8" height="1.8"/>
			</g>
		</g>
	</g>
	<g>
		<g>
			<defs>
				<rect id="SVGID_17_" x="470.1" y="541.1" width="48.9" height="48.9"/>
			</defs>
			<clipPath id="SVGID_18_">
				<use xlink:href="#SVGID_17_"  style="overflow:visible;"/>
			</clipPath>
			<g class="st51">
				<defs>
					<rect id="SVGID_19_" x="470.1" y="541.1" width="48.9" height="48.9"/>
				</defs>
				<clipPath id="SVGID_20_">
					<use xlink:href="#SVGID_19_"  style="overflow:visible;"/>
				</clipPath>
				<path class="st52" d="M513.2,585.5l-0.1-1.7c-0.2-2.7-0.8-8.2-1.4-10.8c-0.7-2.8-1.6-4.8-4.2-6.3l-1-0.6
					c-1.9-1.1-2.7-1.6-3.8-1.6c-0.6,0-1.1,0.1-1.6,0.4l-0.9,0.4l0.7-0.6c2.2-2,3.7-5,3.7-8.4c0-5.9-4.4-10.7-9.8-10.7h0
					c-5.4,0-9.8,4.8-9.8,10.7c0,3.4,1.4,6.4,3.7,8.4l0.7,0.6l-0.9-0.4c-0.5-0.3-1-0.4-1.6-0.4c-1.1,0-1.9,0.5-3.8,1.6l-1,0.6
					c-2.7,1.5-3.6,3.5-4.2,6.3c-0.6,2.6-1.2,8.1-1.4,10.8l-0.1,1.7H513.2z"/>
				<path class="st53" d="M510.1,573.3c-0.6-2.8-1.4-4.1-3.5-5.3c-2.1-1.2-3.2-1.9-4-1.9c-0.3,0-0.6,0.1-0.8,0.2
					c-0.5,0.5-1.1,0.9-1.6,1.2c0,0,0,0,0,0c-0.1,0.1-0.2,0.1-0.3,0.2c-0.6,0.4-1.2,0.6-1.8,0.8c-1.1,0.4-2.2,0.6-3.4,0.6
					c-1.2,0-2.3-0.2-3.4-0.6c-0.6-0.2-1.2-0.4-1.8-0.8c-0.7-0.4-1.3-0.9-1.9-1.4c-0.2-0.1-0.5-0.2-0.8-0.2c-0.8,0-1.6,0.5-4,1.9
					c-2.1,1.2-2.8,2.5-3.5,5.3c-0.6,2.4-1.2,7.9-1.4,10.5h33.6C511.3,581.2,510.6,575.7,510.1,573.3"/>
				<path class="st53" d="M494.7,565.4c-4.5,0-8.2-4.1-8.2-9.1s3.7-9.1,8.2-9.1c4.5,0,8.2,4.1,8.2,9.1S499.2,565.4,494.7,565.4"/>
			</g>
		</g>
	</g>
	<g>
		<g>
			<defs>
				<rect id="SVGID_21_" x="471.3" y="591.4" width="44.9" height="44.9"/>
			</defs>
			<clipPath id="SVGID_22_">
				<use xlink:href="#SVGID_21_"  style="overflow:visible;"/>
			</clipPath>
			<g class="st54">
				<defs>
					<rect id="SVGID_23_" x="471.3" y="591.4" width="44.9" height="44.9"/>
				</defs>
				<clipPath id="SVGID_24_">
					<use xlink:href="#SVGID_23_"  style="overflow:visible;"/>
				</clipPath>
				<path class="st55" d="M489.5,621.2l0.1-1.6c0.1-1.8,0.6-5.6,1-7.3c0.5-2.1,1.1-3.5,3.1-4.6l0.7-0.4c1.3-0.8,2-1.1,2.9-1.1
					c0.5,0,0.9,0.1,1.4,0.3l0.2,0.1l0.2,0.1c0.3,0.3,0.7,0.5,1,0.7c0.3,0.2,0.6,0.3,0.8,0.4l0.1,0c0.6,0.2,1.1,0.3,1.7,0.3
					c0.6,0,1.2-0.1,1.7-0.3c0.3-0.1,0.6-0.2,0.9-0.4l0,0l0.4-0.3l0.1,0c0.2-0.1,0.3-0.2,0.5-0.4l0.2-0.1l0.2-0.1
					c0.4-0.2,0.9-0.3,1.4-0.3c0.9,0,1.6,0.4,2.8,1.1c0.2,0.1,0.5,0.3,0.7,0.4c2,1.1,2.7,2.6,3.1,4.6c0.4,1.7,0.8,5.5,1,7.3l0.1,1.6
					H489.5z"/>
				<path class="st56" d="M512.8,612.6c-0.4-1.8-0.9-2.7-2.3-3.5c-1.4-0.8-2.2-1.3-2.7-1.3c-0.2,0-0.4,0.1-0.6,0.1
					c-0.3,0.3-0.7,0.6-1.1,0.8c0,0,0,0,0,0c-0.1,0-0.1,0.1-0.2,0.1c-0.4,0.2-0.8,0.4-1.2,0.5c-0.7,0.3-1.5,0.4-2.3,0.4
					c-0.8,0-1.6-0.1-2.3-0.4c-0.4-0.1-0.8-0.3-1.2-0.5c-0.5-0.3-0.9-0.6-1.3-0.9c-0.2-0.1-0.3-0.1-0.6-0.1c-0.5,0-1.1,0.4-2.7,1.3
					c-1.4,0.8-1.9,1.7-2.3,3.5c-0.4,1.6-0.8,5.3-0.9,7.1h22.4C513.6,617.9,513.2,614.3,512.8,612.6"/>
				<path class="st55" d="M502.5,609.1c-4,0-7.2-3.5-7.2-7.8c0-4.3,3.2-7.8,7.2-7.8c4,0,7.2,3.5,7.2,7.8
					C509.7,605.6,506.5,609.1,502.5,609.1"/>
				<path class="st56" d="M502.5,607.4c-3,0-5.5-2.7-5.5-6.1c0-3.4,2.5-6.1,5.5-6.1c3,0,5.5,2.7,5.5,6.1
					C508,604.7,505.5,607.4,502.5,607.4"/>
				<path class="st55" d="M472.4,626.7l0.1-1.6c0.1-1.8,0.6-5.6,1-7.3c0.5-2.1,1.1-3.5,3.1-4.6l0.6-0.4c1.3-0.8,2-1.2,2.9-1.2
					c0.5,0,1,0.1,1.4,0.3l0.2,0.1l0.2,0.1c0.3,0.3,0.7,0.5,1,0.7c0.3,0.2,0.6,0.3,0.8,0.4l0.1,0c0.6,0.2,1.1,0.3,1.7,0.3
					c0.6,0,1.2-0.1,1.7-0.3l0.1,0c0.3-0.1,0.5-0.2,0.8-0.4l0.1-0.1l0.4-0.3h0.1c0.2-0.1,0.3-0.2,0.5-0.4l0.2-0.1l0.2-0.1
					c0.4-0.2,0.9-0.3,1.4-0.3c0.9,0,1.6,0.4,2.8,1.1c0.2,0.1,0.5,0.3,0.7,0.4c2,1.1,2.7,2.6,3.1,4.6c0.4,1.8,0.8,5.5,1,7.3l0.1,1.6
					H472.4z"/>
				<path class="st56" d="M495.8,618.1c-0.4-1.8-0.9-2.7-2.3-3.5c-1.4-0.8-2.2-1.3-2.7-1.3c-0.2,0-0.4,0.1-0.6,0.1
					c-0.3,0.3-0.7,0.6-1.1,0.8c0,0,0,0,0,0c-0.1,0-0.1,0.1-0.2,0.1c-0.4,0.2-0.8,0.4-1.2,0.5c-0.7,0.3-1.5,0.4-2.3,0.4
					c-0.8,0-1.6-0.1-2.3-0.4c-0.4-0.1-0.8-0.3-1.2-0.5c-0.5-0.3-0.9-0.6-1.3-0.9c-0.2-0.1-0.3-0.1-0.6-0.1c-0.5,0-1.1,0.4-2.7,1.3
					c-1.4,0.8-1.9,1.7-2.3,3.5c-0.4,1.6-0.8,5.3-0.9,7.1h22.4C496.6,623.4,496.1,619.7,495.8,618.1"/>
				<path class="st55" d="M485.5,614.6c-4,0-7.2-3.5-7.2-7.8c0-4.3,3.2-7.8,7.2-7.8c4,0,7.2,3.5,7.2,7.8
					C492.6,611.1,489.4,614.6,485.5,614.6"/>
				<path class="st56" d="M485.5,612.9c-3,0-5.5-2.7-5.5-6.1c0-3.4,2.5-6.1,5.5-6.1c3,0,5.5,2.7,5.5,6.1
					C490.9,610.1,488.5,612.9,485.5,612.9"/>
				<path class="st55" d="M484.5,634.3l0.1-1.6c0.1-1.8,0.6-5.6,1-7.3c0.5-2.1,1.1-3.5,3.1-4.6l0.6-0.4c1.3-0.8,2-1.1,2.9-1.1
					c0.5,0,1,0.1,1.4,0.3l0.2,0.1l0.2,0.1c0.3,0.3,0.6,0.5,1,0.7c0.3,0.2,0.6,0.3,0.8,0.4l0.1,0c0.6,0.2,1.2,0.3,1.7,0.3
					c0.6,0,1.2-0.1,1.7-0.3l0.1,0c0.3-0.1,0.5-0.2,0.8-0.4l0.1,0l0.4-0.3h0.1c0.2-0.1,0.3-0.2,0.5-0.4l0.2-0.1l0.2-0.1
					c0.4-0.2,0.9-0.3,1.4-0.3c0.9,0,1.6,0.4,2.8,1.1c0.2,0.1,0.5,0.3,0.7,0.4c2,1.1,2.7,2.6,3.1,4.6c0.4,1.7,0.8,5.5,1,7.3l0.1,1.6
					H484.5z"/>
				<path class="st56" d="M507.8,625.8c-0.4-1.8-0.9-2.7-2.3-3.5c-1.4-0.8-2.2-1.3-2.7-1.3c-0.2,0-0.4,0.1-0.6,0.1
					c-0.3,0.3-0.7,0.6-1.1,0.8c0,0,0,0,0,0c-0.1,0-0.1,0.1-0.2,0.1c-0.4,0.2-0.8,0.4-1.2,0.5c-0.7,0.3-1.5,0.4-2.3,0.4
					c-0.8,0-1.6-0.1-2.3-0.4c-0.4-0.1-0.8-0.3-1.2-0.5c-0.5-0.3-0.9-0.6-1.3-0.9c-0.2-0.1-0.3-0.1-0.6-0.1c-0.5,0-1.1,0.4-2.7,1.3
					c-1.4,0.8-1.9,1.7-2.3,3.5c-0.4,1.6-0.8,5.3-0.9,7.1h22.4C508.6,631.1,508.2,627.4,507.8,625.8"/>
				<path class="st55" d="M497.5,622.2c-4,0-7.2-3.5-7.2-7.8c0-4.3,3.2-7.8,7.2-7.8c4,0,7.2,3.5,7.2,7.8
					C504.7,618.7,501.5,622.2,497.5,622.2"/>
				<path class="st56" d="M497.5,620.5c-3,0-5.5-2.7-5.5-6.1c0-3.4,2.5-6.1,5.5-6.1c3,0,5.5,2.7,5.5,6.1
					C503,617.8,500.5,620.5,497.5,620.5"/>
			</g>
		</g>
	</g>
	<g>
		<g>
			<path class="st1" d="M197.8,600.9c-2.3,0-4.3-1.9-4.3-4.2V567c0-2.3,2-4.2,4.3-4.2h40c2.3,0,4.2,1.9,4.2,4.2v29.7
				c0,2.3-1.9,4.2-4.2,4.2H197.8z"/>
		</g>
		<path class="st10" d="M237.9,564.5h-40c-1.4,0-2.6,1.1-2.6,2.5v29.7c0,1.4,1.2,2.5,2.6,2.5h40.1c1.4,0,2.5-1.1,2.5-2.5V567
			C240.4,565.6,239.3,564.5,237.9,564.5z M238.6,596.7c0,0.4-0.3,0.7-0.7,0.7h-40.1c-0.4,0-0.8-0.4-0.8-0.7V567
			c0-0.4,0.4-0.8,0.9-0.8h40c0.4,0,0.7,0.3,0.7,0.7V596.7z"/>
		<g>
			<path class="st10" d="M230.8,587.1v-5.2H230h-0.9h-10.4v-4.3h4.3v-7.8h-10.4v7.8h4.3v4.3h-10.4h-0.9h-0.9v5.2h-3.5v6.9h8.7v-6.9
				h-3.5v-3.5h10.4v3.5h-3.5v6.9h8.7v-6.9h-3.5v-3.5h10.4v3.5h-3.5v6.9h8.7v-6.9H230.8z"/>
		</g>
	</g>
	<g>
		<g>
			<defs>
				<rect id="SVGID_25_" x="333.6" y="561.7" width="52.2" height="52.2"/>
			</defs>
			<clipPath id="SVGID_26_">
				<use xlink:href="#SVGID_25_"  style="overflow:visible;"/>
			</clipPath>
			<g class="st57">
				<defs>
					<rect id="SVGID_27_" x="333.6" y="561.7" width="52.2" height="52.2"/>
				</defs>
				<clipPath id="SVGID_28_">
					<use xlink:href="#SVGID_27_"  style="overflow:visible;"/>
				</clipPath>
				<path class="st58" d="M339.2,608.3v-36.9c0-1.8,1.4-3.2,3.2-3.2h35.3c1.8,0,3.2,1.4,3.2,3.2v36.9H339.2z"/>
				<path class="st59" d="M379.4,606.7v-34.9c0-1.1-0.9-2-2-2h-34.5c-1.1,0-2,0.9-2,2v34.9H379.4z M377.8,605.1h-35.3v-28.9h35.3
					V605.1z"/>
				<rect x="351.2" y="578.6" class="st59" width="4.8" height="4.8"/>
				<rect x="357.7" y="578.6" class="st59" width="4.8" height="4.8"/>
				<rect x="364.1" y="578.6" class="st59" width="4.8" height="4.8"/>
				<rect x="370.5" y="578.6" class="st59" width="4.8" height="4.8"/>
				<rect x="344.8" y="585" class="st59" width="4.8" height="4.8"/>
				<rect x="351.2" y="585" class="st59" width="4.8" height="4.8"/>
				<rect x="357.7" y="585" class="st59" width="4.8" height="4.8"/>
				<rect x="364.1" y="585" class="st59" width="4.8" height="4.8"/>
				<rect x="370.5" y="585" class="st59" width="4.8" height="4.8"/>
				<rect x="344.8" y="591.4" class="st59" width="4.8" height="4.8"/>
				<rect x="351.2" y="591.4" class="st59" width="4.8" height="4.8"/>
				<rect x="357.7" y="591.4" class="st59" width="4.8" height="4.8"/>
				<rect x="364.1" y="591.4" class="st59" width="4.8" height="4.8"/>
				<rect x="370.5" y="591.4" class="st59" width="4.8" height="4.8"/>
				<rect x="344.8" y="597.8" class="st59" width="4.8" height="4.8"/>
				<rect x="351.2" y="597.8" class="st59" width="4.8" height="4.8"/>
				<rect x="357.7" y="597.8" class="st59" width="4.8" height="4.8"/>
				<rect x="364.1" y="597.8" class="st59" width="4.8" height="4.8"/>
			</g>
		</g>
	</g>
	<g>
		<g>
			<defs>
				<rect id="SVGID_29_" x="295" y="536.7" width="60.1" height="60.1"/>
			</defs>
			<clipPath id="SVGID_30_">
				<use xlink:href="#SVGID_29_"  style="overflow:visible;"/>
			</clipPath>
			<rect x="302.4" y="548.8" class="st60" width="45.3" height="36.1"/>
			<path class="st61" d="M304.2,583h41.6v-32.4h-41.6V583z M344,581.1h-37.9v-28.7H344V581.1z"/>
			<rect x="334.7" y="556.2" class="st61" width="5.5" height="6.5"/>
			<rect x="312.5" y="567.2" class="st61" width="16.6" height="1.8"/>
			<rect x="312.5" y="572.8" class="st61" width="21.3" height="1.8"/>
		</g>
	</g>
	<g>
		<g>
			<defs>
				<rect id="SVGID_31_" x="157.3" y="542.1" width="55.2" height="55.2"/>
			</defs>
			<clipPath id="SVGID_32_">
				<use xlink:href="#SVGID_31_"  style="overflow:visible;"/>
			</clipPath>
			<polygon class="st62" points="166.6,592.2 166.6,548 191.1,548 203.1,560.1 203.1,592.2 			"/>
			<path class="st63" d="M201.4,590.5v-29.7l-11-11h-22.1v40.8H201.4z M170,588.8v-37.4h18.7v11h11v26.3H170z"/>
			<rect x="175.9" y="570.1" class="st63" width="17.8" height="1.7"/>
			<rect x="175.9" y="575.2" class="st63" width="17.8" height="1.7"/>
			<rect x="175.9" y="580.3" class="st63" width="17.8" height="1.7"/>
		</g>
	</g>
	<g>
		<path class="st1" d="M370.5,631v-40.4h36V631H370.5z"/>
		<g>
			<path class="st10" d="M396.4,612.3c-0.3-1.5-0.7-2.2-1.8-2.8c-1.1-0.6-1.7-1-2.1-1c-0.2,0-0.3,0-0.4,0.1
				c-0.3,0.2-0.6,0.5-0.9,0.6l0,0c-0.1,0-0.1,0.1-0.2,0.1c-0.3,0.2-0.6,0.3-0.9,0.4c-0.6,0.2-1.2,0.3-1.8,0.3
				c-0.6,0-1.2-0.1-1.8-0.3c-0.3-0.1-0.6-0.2-0.9-0.4c-0.4-0.2-0.7-0.5-1-0.7c-0.1-0.1-0.3-0.1-0.4-0.1c-0.4,0-0.8,0.3-2.1,1
				c-1.1,0.6-1.5,1.3-1.8,2.8c-0.3,1.3-0.6,4.9-0.7,6.3h17.7C397,617.2,396.7,613.6,396.4,612.3z"/>
			<path class="st10" d="M388.3,608.2c-2.4,0-4.3-2.1-4.3-4.8c0-2.6,1.9-4.8,4.3-4.8c2.4,0,4.3,2.1,4.3,4.8
				C392.6,606,390.7,608.2,388.3,608.2z"/>
		</g>
		<path class="st10" d="M372.5,592.6v35h32v-35H372.5z M402.5,622.6h-28v-28h28V622.6z"/>
	</g>
	<g>
		<rect x="305.2" y="602.7" class="st64" width="33.3" height="31.9"/>
		<circle class="st64" cx="335.9" cy="606.7" r="9.3"/>
		<text transform="matrix(1 0 0 1 331.8331 611.0155)" class="st10 st65 st66">1</text>
	</g>
	<g>
		<rect x="167.7" y="602.7" class="st64" width="42.2" height="28.2"/>
		<circle class="st67" cx="188.8" cy="616.7" r="9.3"/>
		<g>
			<g>
				<defs>
					<rect id="SVGID_33_" x="180.9" y="608.1" width="17.8" height="17.8"/>
				</defs>
				<clipPath id="SVGID_34_">
					<use xlink:href="#SVGID_33_"  style="overflow:visible;"/>
				</clipPath>
				<g class="st68">
					<defs>
						<rect id="SVGID_35_" x="180.9" y="608.1" width="17.8" height="17.8"/>
					</defs>
					<clipPath id="SVGID_36_">
						<use xlink:href="#SVGID_35_"  style="overflow:visible;"/>
					</clipPath>
					<path class="st69" d="M184.2,612.2c0-0.4,0.2-0.7,0.5-0.9c0.3-0.2,0.7-0.2,1,0l8.9,4.8c0.4,0.2,0.6,0.5,0.6,0.9
						c0,0.4-0.2,0.7-0.6,0.9l-8.9,4.8c-0.3,0.2-0.7,0.2-1,0c-0.3-0.2-0.5-0.5-0.5-0.9V612.2z"/>
					<path class="st70" d="M185.4,622.3l8.9-4.8c0.4-0.2,0.4-0.6,0-0.8l-8.9-4.8c-0.4-0.2-0.7,0-0.7,0.4v9.7
						C184.7,622.3,185,622.5,185.4,622.3"/>
				</g>
			</g>
		</g>
	</g>
	<circle class="st10" cx="354" cy="492.6" r="4.1"/>
	<circle class="st10" cx="178.6" cy="259.2" r="4.1"/>
	<circle class="st10" cx="295.7" cy="259.2" r="4.1"/>
	<circle class="st10" cx="413" cy="259.2" r="4.1"/>
	<circle class="st7" cx="529.6" cy="218.7" r="4.1"/>
	<text transform="matrix(1 0 0 1 312.4307 340.2214)" class="st1 st2 st3">v2.0 app model</text>
	<g>
		<polygon class="st71" points="173,129.6 159.1,118.7 172.3,101.9 186.4,118.7 		"/>
		<circle class="st21" cx="172.7" cy="110.3" r="2"/>
		<circle class="st21" cx="166.6" cy="117.7" r="2"/>
		<circle class="st21" cx="178.5" cy="117.7" r="2"/>
		<circle class="st21" cx="172.7" cy="122.8" r="2"/>
		<line class="st72" x1="172.7" y1="110.3" x2="172.7" y2="122.8"/>
		<line class="st72" x1="172.7" y1="110.3" x2="166.6" y2="117.7"/>
		<line class="st72" x1="172.7" y1="110.3" x2="178.5" y2="117.7"/>
		<line class="st72" x1="166.6" y1="117.7" x2="172.7" y2="123.5"/>
		<line class="st72" x1="172.7" y1="123.5" x2="178.5" y2="117.7"/>
	</g>
	<g>
		<polygon class="st71" points="145.3,394.4 131.4,383.5 144.7,366.7 158.7,383.5 		"/>
		<circle class="st21" cx="145" cy="375.1" r="2"/>
		<circle class="st21" cx="138.9" cy="382.5" r="2"/>
		<circle class="st21" cx="150.8" cy="382.5" r="2"/>
		<circle class="st21" cx="145" cy="387.6" r="2"/>
		<line class="st72" x1="145" y1="375.1" x2="145" y2="387.6"/>
		<line class="st72" x1="145" y1="375.1" x2="138.9" y2="382.5"/>
		<line class="st72" x1="145" y1="375.1" x2="150.8" y2="382.5"/>
		<line class="st72" x1="138.9" y1="382.5" x2="145" y2="388.4"/>
		<line class="st72" x1="145" y1="388.4" x2="150.8" y2="382.5"/>
	</g>
	<g>
		<g>
			<defs>
				<rect id="SVGID_37_" x="419.4" y="17.1" width="26.5" height="26.5"/>
			</defs>
			<clipPath id="SVGID_38_">
				<use xlink:href="#SVGID_37_"  style="overflow:visible;"/>
			</clipPath>
			<polygon class="st73" points="430.8,30.1 430.8,22.1 422.7,23.2 422.7,30.1 			"/>
			<polygon class="st73" points="431.2,30.1 442.7,30.1 442.7,20.3 431.2,22 			"/>
			<polygon class="st73" points="431.2,30.6 431.2,38.7 442.7,40.4 442.7,30.6 			"/>
			<polygon class="st73" points="430.8,30.6 422.7,30.6 422.7,37.5 430.8,38.6 			"/>
		</g>
	</g>
	<text transform="matrix(1 0 0 1 516.4418 38.8259)" class="st1 st2 st29">...</text>
	<rect x="451" y="23.3" class="st74" width="38.5" height="16"/>
	<text transform="matrix(1 0 0 1 451.0208 38.3713)" class="st1 st75 st29">iOS</text>
	<g>
		<path class="st21" d="M496.9,32.9c0,0.6-0.5,1.2-1.1,1.2c-0.6,0-1.1-0.5-1.1-1.2V27c0-0.6,0.5-1.2,1.1-1.2c0.6,0,1.1,0.5,1.1,1.2
			V32.9L496.9,32.9L496.9,32.9z"/>
		<path class="st21" d="M512.9,32.9c0,0.6-0.5,1.2-1.1,1.2s-1.1-0.5-1.1-1.2V27c0-0.6,0.5-1.2,1.1-1.2c0.6,0,1.1,0.5,1.1,1.2V32.9
			L512.9,32.9L512.9,32.9z"/>
		<path class="st21" d="M498,25.8v8.7c0,1,0.7,1.8,1.6,1.8h0.7v3c0,0.6,0.5,1.2,1.1,1.2c0.6,0,1.1-0.5,1.1-1.2v-3h2.3v3
			c0,0.6,0.5,1.2,1.1,1.2s1.1-0.5,1.1-1.2v-3h1.1c0.9,0,1.3-0.8,1.3-1.8v-8.7H498L498,25.8L498,25.8z"/>
		<path class="st21" d="M510,24.5c0,0,0-0.1,0-0.2c0-3.1-2.8-5.6-6.2-5.6c-3.4,0-6.2,2.5-6.2,5.6c0,0.1,0,0.2,0,0.2H510L510,24.5
			L510,24.5z"/>
		<path class="st21" d="M501.6,20.8c0.1,0.1,0,0.3-0.1,0.4c-0.1,0.1-0.3,0-0.4-0.1l-1.7-3.1c-0.1-0.1,0-0.3,0.1-0.4
			c0.1-0.1,0.3,0,0.4,0.1L501.6,20.8L501.6,20.8L501.6,20.8z"/>
		<path class="st21" d="M505.9,20.8c-0.1,0.1,0,0.3,0.1,0.4c0.1,0.1,0.3,0,0.4-0.1l1.7-3.1c0.1-0.1,0-0.3-0.1-0.4
			c-0.1-0.1-0.3,0-0.4,0.1L505.9,20.8L505.9,20.8L505.9,20.8z"/>
		<path class="st76" d="M501.5,21.7c0,0.3-0.3,0.6-0.6,0.6c-0.3,0-0.6-0.3-0.6-0.6s0.3-0.6,0.6-0.6
			C501.3,21.1,501.5,21.4,501.5,21.7L501.5,21.7z"/>
		<path class="st76" d="M507.2,21.7c0-0.3-0.3-0.6-0.6-0.6c-0.3,0-0.6,0.3-0.6,0.6s0.3,0.6,0.6,0.6C507,22.3,507.2,22,507.2,21.7
			L507.2,21.7z"/>
	</g>
	<g>
		<g>
			<path class="st1" d="M239.4,614.8c0-1.2-1-2.2-2.2-2.2h-0.3v-0.2c0-1.2-1-2.2-2.2-2.2H225v-3.8h-1.4l-22.4,3.9v31.4l22.4,3.9h1.4
				v-3.8h9.6c1.1,0,2-0.8,2.2-1.9h0.3c1.2,0,2.2-1,2.2-2.2v-7c0-0.2,0-0.5-0.1-0.7c0.1-0.2,0.1-0.4,0.1-0.7V623c0-0.2,0-0.5-0.1-0.7
				c0.1-0.2,0.1-0.5,0.1-0.7V614.8z"/>
			<path class="st10" d="M238.1,614.8c0-0.5-0.4-1-1-1h-1.5v-1.5c0-0.5-0.4-1-1-1h-10.8v-3.8l-21.2,3.7v29.3l21.2,3.7v-3.8v0h10.8
				c0.5,0,1-0.4,1-1v-0.9h1.5c0.5,0,1-0.4,1-1v-7c0-0.3-0.1-0.5-0.3-0.7c0.2-0.2,0.3-0.4,0.3-0.7V623c0-0.3-0.1-0.5-0.3-0.7
				c0.2-0.2,0.3-0.4,0.3-0.7V614.8z M236.9,637.2c0,0.2-0.1,0.3-0.3,0.3h-0.9v-6.9h0.9c0.2,0,0.3,0.1,0.3,0.3V637.2z M236.9,629.1
				c0,0.2-0.1,0.3-0.3,0.3h-0.9v-6.9h0.9c0.2,0,0.3,0.1,0.3,0.3V629.1z M236.9,621.1c0,0.1-0.1,0.3-0.3,0.3h-2.2v18.1h-10.6v-26.8
				h10.6v2.5h2.2c0.1,0,0.3,0.1,0.3,0.3V621.1z"/>
		</g>
		<g>
			<rect x="221.9" y="615.2" class="st10" width="10" height="1.7"/>
			<rect x="221.9" y="619" class="st10" width="10" height="1.7"/>
			<rect x="221.9" y="622.7" class="st10" width="10" height="1.7"/>
			<rect x="221.9" y="626.5" class="st10" width="10" height="1.7"/>
			<rect x="221.9" y="630.2" class="st10" width="10" height="1.7"/>
			<rect x="221.9" y="634" class="st10" width="10" height="1.7"/>
		</g>
	</g>
</g>
</svg>





<!--
<a name="PlannerAPIIntro"> </a>

###Planner API (preview)

The Planner API enables you to create light-weight project management solutions that create and manage projects, assign project tasks to users, and track the progress and completion of those tasks.

Additional value-prop or technical information about the Planner API, so that developers can decide if they want to know even more. Maybe a paragraph or two at most.

For more information, see [link to Planner API topic].
-->

###Support for the v2.0 app authentication model preview

The v2.0 app authentication model preview enables you to create apps that accept both work and school (Azure AD) as well as personal (Microsoft account) identities. 

In the past, an app developer who wanted to support both Microsoft accounts and Azure Active Directory was required to integrate with two completely separate systems. Now you can build apps using the v2.0 application model, which allows you to sign users in with both types of accounts. 

Currently, your apps can access the following APIs using the v2.0 app authentication model preview:

- Outlook mail 
- Outlook contacts 
- Outlook calendars

For more information, see [Authenticate Office 365 and Outlook.com APIs using the v2.0 app model preview](..\howto\authenticate-Office-365-APIs-using-v2.md).

<a name="OfficeGraphIntro"> </a>

###Office Graph 
The Office Graph stores data _about_ Office 365 entities and the relationships between them as nodes and edges in a graph index. Examples of enterprise entities are **person** and **document**; examples of relationships are **shared** and **modified**. 

The Office Graph uses advanced analytics and machine learning techniques to connect and complete the data coming from all of the Office 365 services. 

Currently there are two relationships available for preview: **TrendingAround** and **WorkingWith**. See [Develop with the Office Graph](https://msdn.microsoft.com/office/office365/howto/develop-office-graph) for examples of how you can query for these relationships. 

<!-- no longer in preview

###Outlook Notifications REST API (preview)
The Notifications API provides change notifications for entities like mail, contacts, events, and groups in Office 365. 
These push notifications use the concept of webhooks as a callback mechanism to provide the change notifications.
During the Preview period, you can access this API at the REST endpoint https://outlook.office365.com/api/beta/{user_context}.

For more information see [Outlook Notifications REST API reference (preview)](../api/notify-rest-operations.md).   

###Outlook User Photo REST API (preview)

The User Photo API allows you to get information about and download the photo of any user in your organization. 
During the Preview period, you can access this API at the REST endpoint https://outlook.office365.com/api/beta/{user_context}.

For more information, see [Outlook User Photo REST API reference (preview)](../api/photo-rest-operations.md).

-->

###Using multiple preview features in a solution

Because preview features are still under development, there may be instances where a given preview feature may not yet completely integrate with or support other preview features. In general, refer to the documentation for a specific preview feature for information on how it inter-operates with or supports other preview features.

##Other preview features in the Office 365 development platform

In addition to the Preview APIs in the Office 365 API listed above, we've made available the following preview features to the larger Office 365 development platform:

###Service Communications API (preview)

The new version of the Office 365 Service Communications API provides service health information to Office 365 tenant administrators and partners via REST APIs. For operations reference, see [Office 365 Service Communications API reference (preview)](https://msdn.microsoft.com/library/office/dn707386.aspx).

###Management Activity API (preview)

The Office 365 Management Activity API provides information about user, admin, system, and policy actions and events from Office 365 and Azure Active Directory activity logs to Office 365 tenant administrators and partners via REST APIs. For operations reference, see [Office 365 Management Activity API reference (preview)](https://msdn.microsoft.com/library/office/mt227394.aspx).

