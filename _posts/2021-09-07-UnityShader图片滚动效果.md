---
layout: post
title: Unity Shader 图片滚动效果
categories: Unity3D
description: 在unity中的shader实现图片无限滚动的效果,可以用做引导的箭头.
keywords: Unity3D,U3D,Shader
---
## Unity Shader 图片滚动效果

## **要透明就效果就不要把图片格式设置成Sprite,用默认的格式就可以有透明效果**

## **要透明就效果就不要把图片格式设置成Sprite,用默认的格式就可以有透明效果**

## **要透明就效果就不要把图片格式设置成Sprite,用默认的格式就可以有透明效果**

```c#
// Upgrade NOTE: replaced 'mul(UNITY_MATRIX_MVP,*)' with 'UnityObjectToClipPos(*)'

Shader "UnityShaders/UVAnimation" {
	Properties {
		_Color ("Color Tint", Color) = (1, 1, 1, 1)
		_MainTex ("Image Sequence", 2D) = "white" {}

    	_Speed ("Speed", Range(-10, 10)) = 1
	}
	SubShader {
		Tags {"Queue"="Transparent" "IgnoreProjector"="True" "RenderType"="Transparent"}
		
		Pass {
			Tags { "LightMode"="ForwardBase" }
			
			ZWrite Off
			Blend SrcAlpha OneMinusSrcAlpha
			
			CGPROGRAM
			
			#pragma vertex vert  
			#pragma fragment frag
			
			#include "UnityCG.cginc"
			
			fixed4 _Color;
			sampler2D _MainTex;
			float4 _MainTex_ST;
	
			float _Speed;
			  
			struct a2v {  
			    float4 vertex : POSITION; 
			    float2 texcoord : TEXCOORD0;
			};  
			
			struct v2f {  
			    float4 pos : SV_POSITION;
			    float2 uv : TEXCOORD0;
			};  
			
			v2f vert (a2v v) {  
				v2f o;  
				o.pos = UnityObjectToClipPos(v.vertex);  
				o.uv = TRANSFORM_TEX(v.texcoord, _MainTex);  
				return o;
			}  
			
			fixed4 frag (v2f i) : SV_Target {
				
				half2 uv = i.uv;
				uv.x += (_Time.y * _Speed);
				//uv.y  += time;;
				
				fixed4 c = tex2D(_MainTex, uv);
				c.rgb *= _Color;
				
				return c;
			}
			
			ENDCG
		}  
	}
	FallBack "Transparent/VertexLit"
}
```

![image](..\images\blog\UnityShaderUVAnimation.gif)